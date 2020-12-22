<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# About

I am a fifth year undergraduate student at Georgia Tech, majoring in
mathematics and computer science.

## Contact

You can reach me at `dprofili3 at gatech dot edu` or `dprofili at
protonmail dot com`.

# Research

## Tropical resultants

Suppose we have polynomials $$f_1, \dots, f_n \in \mathbb{C}[x_1,
\dots, x_m],$$ each of the form

$$f_i = b_{i, 1} x_1^{a_{i,1}} + \dots + b_{i, m} x_m^{a_{i, m}},,$$

where $$b_{i,k} \in \mathbb{C}$$ and $$a_{i, k} \in \mathbb{Z}.$$ What
can we say about the choices of coefficients $$b_{i,k}$$ which satisfy
$$f_1 = \dots = f_n = 0$$?

As it turns out, there is a unique polynomial called the *resultant*
which is defined as a polynomial $$R$$ of
the coefficients such that $$R(b_{1,1}, \dots, b_{n, m}) = 0$$ if and
only if the $$b_{i, j}$$'s satisfy $$f_1 = \dots = f_n = 0$$. 

<iframe srcdoc="<!DOCTYPE html>
<html>
<head><meta charset="utf-8" />

<title>example</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>




<body>

<script src=&quot;/nbextensions/threejs/build/three.min.js&quot;></script>
<script>
  if ( !window.THREE ) document.write(' \
<script src=&quot;https://cdn.jsdelivr.net/gh/sagemath/threejs-sage@r123/build/three.min.js&quot;><\/script> \
            ');
</script>
        
<script>

    var scene = new THREE.Scene();

    var renderer = new THREE.WebGLRenderer( { antialias: true, preserveDrawingBuffer: true } );
    renderer.setPixelRatio( window.devicePixelRatio );
    renderer.setSize( window.innerWidth, window.innerHeight );
    renderer.setClearColor( 0xffffff, 1 );
    document.body.appendChild( renderer.domElement );

    var options = {&quot;animate&quot;: false, &quot;animationControls&quot;: true, &quot;aspectRatio&quot;: [1.0, 1.0, 1.0], &quot;autoPlay&quot;: true, &quot;axes&quot;: false, &quot;axesLabels&quot;: [&quot;x&quot;, &quot;y&quot;, &quot;z&quot;], &quot;decimals&quot;: 2, &quot;delay&quot;: 20, &quot;frame&quot;: true, &quot;loop&quot;: true, &quot;projection&quot;: &quot;perspective&quot;, &quot;viewpoint&quot;: false};
    var animate = options.animate;

    var b = [{&quot;x&quot;:-0.873231199259882, &quot;y&quot;:-1.1643082656798427, &quot;z&quot;:-1.1643082656798427}, {&quot;x&quot;:0.4824890149793509, &quot;y&quot;:0.46594069822187095, &quot;z&quot;:0.46594069822187095}]; // bounds

    if ( b[0].x === b[1].x ) {
        b[0].x -= 1;
        b[1].x += 1;
    }
    if ( b[0].y === b[1].y ) {
        b[0].y -= 1;
        b[1].y += 1;
    }
    if ( b[0].z === b[1].z ) {
        b[0].z -= 1;
        b[1].z += 1;
    }

    var rRange = Math.sqrt( Math.pow( b[1].x - b[0].x, 2 )
                            + Math.pow( b[1].y - b[0].y, 2 ) );
    var xRange = b[1].x - b[0].x;
    var yRange = b[1].y - b[0].y;
    var zRange = b[1].z - b[0].z;

    var ar = options.aspectRatio;
    var a = [ ar[0], ar[1], ar[2] ]; // aspect multipliers
    var autoAspect = 2.5;
    if ( zRange > autoAspect * rRange && a[2] === 1 ) a[2] = autoAspect * rRange / zRange;

    // Distance from (xMid,yMid,zMid) to any corner of the bounding box, after applying aspectRatio
    var midToCorner = Math.sqrt( a[0]*a[0]*xRange*xRange + a[1]*a[1]*yRange*yRange + a[2]*a[2]*zRange*zRange ) / 2;

    var xMid = ( b[0].x + b[1].x ) / 2;
    var yMid = ( b[0].y + b[1].y ) / 2;
    var zMid = ( b[0].z + b[1].z ) / 2;

    var box = new THREE.Geometry();
    box.vertices.push( new THREE.Vector3( a[0]*b[0].x, a[1]*b[0].y, a[2]*b[0].z ) );
    box.vertices.push( new THREE.Vector3( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) );
    var boxMesh = new THREE.Line( box );
    if ( options.frame ) scene.add( new THREE.BoxHelper( boxMesh, 'black' ) );

    if ( options.axesLabels ) {

        var d = options.decimals; // decimals
        var offsetRatio = 0.1;
        var al = options.axesLabels;

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var xm = xMid.toFixed(d);
        if ( /^-0.?0*$/.test(xm) ) xm = xm.substr(1);
        addLabel( al[0] + '=' + xm, a[0]*xMid, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[0].x ).toFixed(d), a[0]*b[0].x, a[1]*b[1].y+offset, a[2]*b[0].z );
        addLabel( ( b[1].x ).toFixed(d), a[0]*b[1].x, a[1]*b[1].y+offset, a[2]*b[0].z );

        var offset = offsetRatio * a[0]*( b[1].x - b[0].x );
        var ym = yMid.toFixed(d);
        if ( /^-0.?0*$/.test(ym) ) ym = ym.substr(1);
        addLabel( al[1] + '=' + ym, a[0]*b[1].x+offset, a[1]*yMid, a[2]*b[0].z );
        addLabel( ( b[0].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[0].y, a[2]*b[0].z );
        addLabel( ( b[1].y ).toFixed(d), a[0]*b[1].x+offset, a[1]*b[1].y, a[2]*b[0].z );

        var offset = offsetRatio * a[1]*( b[1].y - b[0].y );
        var zm = zMid.toFixed(d);
        if ( /^-0.?0*$/.test(zm) ) zm = zm.substr(1);
        addLabel( al[2] + '=' + zm, a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*zMid );
        addLabel( ( b[0].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[0].z );
        addLabel( ( b[1].z ).toFixed(d), a[0]*b[1].x, a[1]*b[0].y-offset, a[2]*b[1].z );

    }

    function addLabel( text, x, y, z, color='black', fontSize=14, fontFamily='monospace',
                       fontStyle='normal', fontWeight='normal', opacity=1 ) {

        var canvas = document.createElement( 'canvas' );
        var context = canvas.getContext( '2d' );
        var pixelRatio = Math.round( window.devicePixelRatio );

        var font = [fontStyle, fontWeight, fontSize + 'px', fontFamily].join(' ');

        context.font = font;
        var width = context.measureText( text ).width;
        var height = fontSize;

        // The dimensions of the canvas's underlying image data need to be powers
        // of two in order for the resulting texture to support mipmapping.
        canvas.width = THREE.MathUtils.ceilPowerOfTwo( width * pixelRatio );
        canvas.height = THREE.MathUtils.ceilPowerOfTwo( height * pixelRatio );

        // Re-compute the unscaled dimensions after the power of two conversion.
        width = canvas.width / pixelRatio;
        height = canvas.height / pixelRatio;

        canvas.style.width = width + 'px';
        canvas.style.height = height + 'px';

        context.scale( pixelRatio, pixelRatio );
        context.fillStyle = color;
        context.font = font; // Must be set again after measureText.
        context.textAlign = 'center';
        context.textBaseline = 'middle';
        context.fillText( text, width/2, height/2 );

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var materialOptions = { map: texture, sizeAttenuation: false };
        if ( opacity < 1 ) {
            // Setting opacity=1 would cause the texture's alpha component to be
            // discarded, giving the text a black background instead of the
            // background being transparent.
            materialOptions.opacity = opacity;
        }
        var sprite = new THREE.Sprite( new THREE.SpriteMaterial( materialOptions ) );
        sprite.position.set( x, y, z );

        // Scaling factor, chosen somewhat arbitrarily so that the size of the text
        // is consistent with previously generated plots.
        var scale = 1/625;
        if ( options.projection === 'orthographic' ) {
            scale = midToCorner/256; // Needs to scale along with the plot itself.
        }
        sprite.scale.set( scale * width, scale * height, 1 );

        scene.add( sprite );

        return sprite;

    }

    if ( options.axes ) scene.add( new THREE.AxesHelper( Math.min( a[0]*b[1].x, a[1]*b[1].y, a[2]*b[1].z ) ) );

    var camera = createCamera();
    camera.up.set( 0, 0, 1 );
    camera.position.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );

    var offset = new THREE.Vector3( a[0]*xRange, a[1]*yRange, a[2]*zRange );

    if ( options.viewpoint ) {

        var aa = options.viewpoint;
        var axis = new THREE.Vector3( aa[0][0], aa[0][1], aa[0][2] ).normalize();
        var angle = aa[1] * Math.PI / 180;
        var q = new THREE.Quaternion().setFromAxisAngle( axis, angle ).inverse();

        offset.set( 0, 0, offset.length() );
        offset.applyQuaternion( q );

    }

    camera.position.add( offset );

    function createCamera() {

        var aspect = window.innerWidth / window.innerHeight;

        if ( options.projection === 'orthographic' ) {
            var camera = new THREE.OrthographicCamera( -1, 1, 1, -1, -1000, 1000 );
            updateCameraAspect( camera, aspect );
            return camera;
        }

        return new THREE.PerspectiveCamera( 45, aspect, 0.1, 1000 );

    }

    function updateCameraAspect( camera, aspect ) {

        if ( camera.isPerspectiveCamera ) {
            camera.aspect = aspect;
        } else if ( camera.isOrthographicCamera ) {
            // Fit the camera frustum to the bounding box's diagonal so that the entire plot fits
            // within at the default zoom level and camera position.
            if ( aspect > 1 ) { // Wide window
                camera.top = midToCorner;
                camera.right = midToCorner * aspect;
            } else { // Tall or square window
                camera.top = midToCorner / aspect;
                camera.right = midToCorner;
            }
            camera.bottom = -camera.top;
            camera.left = -camera.right;
        }

        camera.updateProjectionMatrix();

    }

    var lights = [{&quot;x&quot;:-5, &quot;y&quot;:3, &quot;z&quot;:0, &quot;color&quot;:&quot;#7f7f7f&quot;, &quot;parent&quot;:&quot;camera&quot;}];
    for ( var i=0 ; i < lights.length ; i++ ) {
        var light = new THREE.DirectionalLight( lights[i].color, 1 );
        light.position.set( a[0]*lights[i].x, a[1]*lights[i].y, a[2]*lights[i].z );
        if ( lights[i].parent === 'camera' ) {
            light.target.position.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
            scene.add( light.target );
            camera.add( light );
        } else scene.add( light );
    }
    scene.add( camera );

    var ambient = {&quot;color&quot;:&quot;#7f7f7f&quot;};
    scene.add( new THREE.AmbientLight( ambient.color, 1 ) );

    var controls = new THREE.OrbitControls( camera, renderer.domElement );
    controls.target.set( a[0]*xMid, a[1]*yMid, a[2]*zMid );
    controls.addEventListener( 'change', function() { if ( !animate ) render(); } );

    window.addEventListener( 'resize', function() {

        renderer.setSize( window.innerWidth, window.innerHeight );
        updateCameraAspect( camera, window.innerWidth / window.innerHeight );
        if ( !animate ) render();

    } );

    var texts = [];
    for ( var i=0 ; i < texts.length ; i++ ) addText( texts[i] );

    function addText( json ) {
        json.fontFamily = json.fontFamily.map( function( f ) {
            // Need to put quotes around fonts that have whitespace in their names.
            return /\s/.test( f ) ? '&quot;' + f + '&quot;' : f;
        }).join(', ');
        var sprite = addLabel( json.text, a[0]*json.x, a[1]*json.y, a[2]*json.z, json.color,
                               json.fontSize, json.fontFamily, json.fontStyle, json.fontWeight,
                               json.opacity );
        sprite.userData = json;
    }

    var points = [{&quot;point&quot;: [-0.27956441893312256, 0.46594069822187095, 0.46594069822187095], &quot;size&quot;: 5.0, &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0}, {&quot;point&quot;: [-0.38804915564986625, -0.905448029849688, 0.25869943709991094], &quot;size&quot;: 5.0, &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0}, {&quot;point&quot;: [-0.38804915564986625, 0.25869943709991094, -0.905448029849688], &quot;size&quot;: 5.0, &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0}, {&quot;point&quot;: [-0.873231199259882, -1.1643082656798427, -1.1643082656798427], &quot;size&quot;: 5.0, &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0}, {&quot;point&quot;: [0.43696810382742324, -0.07282801730457054, -0.07282801730457054], &quot;size&quot;: 5.0, &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0}, {&quot;point&quot;: [0.4824890149793509, 0.40207417914945903, 0.40207417914945903], &quot;size&quot;: 5.0, &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0}];
    for ( var i=0 ; i < points.length ; i++ ) addPoint( points[i] );

    function addPoint( json ) {

        var geometry = new THREE.Geometry();
        var v = json.point;
        geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );

        var canvas = document.createElement( 'canvas' );
        canvas.width = 128;
        canvas.height = 128;

        var context = canvas.getContext( '2d' );
        context.arc( 64, 64, 64, 0, 2 * Math.PI );
        context.fillStyle = json.color;
        context.fill();

        var texture = new THREE.Texture( canvas );
        texture.needsUpdate = true;

        var transparent = json.opacity < 1 ? true : false;
        var size = camera.isOrthographicCamera ? json.size : json.size/100;
        var material = new THREE.PointsMaterial( { size: size, map: texture,
                                                   transparent: transparent, opacity: json.opacity,
                                                   alphaTest: .1 } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Points( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        mesh.userData = json;
        scene.add( mesh );

    }

    var lines = [{&quot;points&quot;: [[-0.27956441893312256, 0.46594069822187095, 0.46594069822187095], [-0.38804915564986625, -0.905448029849688, 0.25869943709991094]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[-0.27956441893312256, 0.46594069822187095, 0.46594069822187095], [-0.38804915564986625, 0.25869943709991094, -0.905448029849688]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[-0.27956441893312256, 0.46594069822187095, 0.46594069822187095], [-0.873231199259882, -1.1643082656798427, -1.1643082656798427]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[-0.27956441893312256, 0.46594069822187095, 0.46594069822187095], [0.43696810382742324, -0.07282801730457054, -0.07282801730457054]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[-0.27956441893312256, 0.46594069822187095, 0.46594069822187095], [0.4824890149793509, 0.40207417914945903, 0.40207417914945903]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[-0.38804915564986625, -0.905448029849688, 0.25869943709991094], [-0.38804915564986625, 0.25869943709991094, -0.905448029849688]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[-0.38804915564986625, -0.905448029849688, 0.25869943709991094], [-0.873231199259882, -1.1643082656798427, -1.1643082656798427]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[-0.38804915564986625, -0.905448029849688, 0.25869943709991094], [0.43696810382742324, -0.07282801730457054, -0.07282801730457054]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[-0.38804915564986625, -0.905448029849688, 0.25869943709991094], [0.4824890149793509, 0.40207417914945903, 0.40207417914945903]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[-0.38804915564986625, 0.25869943709991094, -0.905448029849688], [-0.873231199259882, -1.1643082656798427, -1.1643082656798427]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[-0.38804915564986625, 0.25869943709991094, -0.905448029849688], [0.43696810382742324, -0.07282801730457054, -0.07282801730457054]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[-0.38804915564986625, 0.25869943709991094, -0.905448029849688], [0.4824890149793509, 0.40207417914945903, 0.40207417914945903]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[-0.873231199259882, -1.1643082656798427, -1.1643082656798427], [0.43696810382742324, -0.07282801730457054, -0.07282801730457054]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[-0.873231199259882, -1.1643082656798427, -1.1643082656798427], [0.4824890149793509, 0.40207417914945903, 0.40207417914945903]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}, {&quot;points&quot;: [[0.43696810382742324, -0.07282801730457054, -0.07282801730457054], [0.4824890149793509, 0.40207417914945903, 0.40207417914945903]], &quot;color&quot;: &quot;#0000ff&quot;, &quot;opacity&quot;: 1.0, &quot;linewidth&quot;: 1.0}];
    for ( var i=0 ; i < lines.length ; i++ ) addLine( lines[i] );

    function addLine( json ) {

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.points.length ; i++ ) {
            var v = json.points[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v[0], a[1]*v[1], a[2]*v[2] ) );
        }

        var transparent = json.opacity < 1 ? true : false;
        var material = new THREE.LineBasicMaterial( { color: json.color, linewidth: json.linewidth,
                                                      transparent: transparent, opacity: json.opacity } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Line( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        mesh.userData = json;
        scene.add( mesh );

    }

    var surfaces = [{&quot;vertices&quot;: [], &quot;faces&quot;: [], &quot;color&quot;: &quot;#008000&quot;, &quot;opacity&quot;: 1.0}];
    for ( var i=0 ; i < surfaces.length ; i++ ) addSurface( surfaces[i] );

    function addSurface( json ) {

        var useFaceColors = 'faceColors' in json ? true : false;

        var geometry = new THREE.Geometry();
        for ( var i=0 ; i < json.vertices.length ; i++ ) {
            var v = json.vertices[i];
            geometry.vertices.push( new THREE.Vector3( a[0]*v.x, a[1]*v.y, a[2]*v.z ) );
        }
        for ( var i=0 ; i < json.faces.length ; i++ ) {
            var f = json.faces[i];
            for ( var j=0 ; j < f.length - 2 ; j++ ) {
                var face = new THREE.Face3( f[0], f[j+1], f[j+2] );
                if ( useFaceColors ) face.color.set( json.faceColors[i] );
                geometry.faces.push( face );
            }
        }
        geometry.computeVertexNormals();

        var side = json.singleSide ? THREE.FrontSide : THREE.DoubleSide;
        var transparent = json.opacity < 1 ? true : false;
        var flatShading = json.useFlatShading ? json.useFlatShading : false;

        var material = new THREE.MeshPhongMaterial( { side: side,
                                     color: useFaceColors ? 'white' : json.color,
                                     vertexColors: useFaceColors ? THREE.FaceColors : THREE.NoColors,
                                     transparent: transparent, opacity: json.opacity,
                                     shininess: 20, flatShading: flatShading } );

        var c = new THREE.Vector3();
        geometry.computeBoundingBox();
        geometry.boundingBox.getCenter( c );
        geometry.translate( -c.x, -c.y, -c.z );

        var mesh = new THREE.Mesh( geometry, material );
        mesh.position.set( c.x, c.y, c.z );
        if ( transparent && json.renderOrder ) mesh.renderOrder = json.renderOrder;
        mesh.userData = json;
        scene.add( mesh );

        if ( json.showMeshGrid ) {

            var geometry = new THREE.Geometry();

            for ( var i=0 ; i < json.faces.length ; i++ ) {
                var f = json.faces[i];
                for ( var j=0 ; j < f.length ; j++ ) {
                    var k = j === f.length-1 ? 0 : j+1;
                    var v1 = json.vertices[f[j]];
                    var v2 = json.vertices[f[k]];
                    // vertices in opposite directions on neighboring faces
                    var nudge = f[j] < f[k] ? .0005*zRange : -.0005*zRange;
                    geometry.vertices.push( new THREE.Vector3( a[0]*v1.x, a[1]*v1.y, a[2]*(v1.z+nudge) ) );
                    geometry.vertices.push( new THREE.Vector3( a[0]*v2.x, a[1]*v2.y, a[2]*(v2.z+nudge) ) );
                }
            }

            var material = new THREE.LineBasicMaterial( { color: 'black', linewidth: 1 } );

            var c = new THREE.Vector3();
            geometry.computeBoundingBox();
            geometry.boundingBox.getCenter( c );
            geometry.translate( -c.x, -c.y, -c.z );

            var mesh = new THREE.LineSegments( geometry, material );
            mesh.position.set( c.x, c.y, c.z );
            mesh.userData = json;
            scene.add( mesh );

        }

    }

    function render() {

        if ( window.updateAnimation ) animate = updateAnimation();
        if ( animate ) requestAnimationFrame( render );

        renderer.render( scene, camera );

    }

    render();
    controls.update();
    if ( !animate ) render();


    // menu functions

    function toggleMenu() {

        var m = document.getElementById( 'menu-content' );
        if ( m.style.display === 'block' ) m.style.display = 'none'
        else m.style.display = 'block';

    }


    function saveAsPNG() {

        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = renderer.domElement.toDataURL( 'image/png' );
        a.download = 'screenshot';
        a.click();

    }

    function saveAsHTML() {

        toggleMenu(); // otherwise visible in output
        event.stopPropagation();

        var blob = new Blob( [ '<!DOCTYPE html>\n' + document.documentElement.outerHTML ] );
        var a = document.body.appendChild( document.createElement( 'a' ) );
        a.href = window.URL.createObjectURL( blob );
        a.download = 'graphic.html';
        a.click();

    }

    function getViewpoint() {

        function roundTo( x, n ) { return +x.toFixed(n); }

        var v = camera.quaternion.inverse();
        var r = Math.sqrt( v.x*v.x + v.y*v.y + v.z*v.z );
        var axis = [ roundTo( v.x / r, 4 ), roundTo( v.y / r, 4 ), roundTo( v.z / r, 4 ) ];
        var angle = roundTo( 2 * Math.atan2( r, v.w ) * 180 / Math.PI, 2 );

        var textArea = document.createElement( 'textarea' );
        textArea.textContent = JSON.stringify( axis ) + ',' + angle;
        textArea.style.csstext = 'position: absolute; top: -100%';
        document.body.append( textArea );
        textArea.select();
        document.execCommand( 'copy' );

        var m = document.getElementById( 'menu-message' );
        m.innerHTML = 'Viewpoint copied to clipboard';
        m.style.display = 'block';
        setTimeout( function() { m.style.display = 'none'; }, 2000 );

    }

</script>

<div id=&quot;menu-container&quot; onclick=&quot;toggleMenu()&quot;>&#x24d8;
<div id=&quot;menu-message&quot;></div>
<div id=&quot;menu-content&quot;>
<div onclick=&quot;saveAsPNG()&quot;>Save as PNG</div>
<div onclick=&quot;saveAsHTML()&quot;>Save as HTML</div>
<div onclick=&quot;getViewpoint()&quot;>Get Viewpoint</div>
<div>Close Menu</div>
</div></div>


</body>
</html>
"
        width="100%"
        height="400"
        style="border: 0;">
</iframe>

</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span> 
</pre></div>

    </div>
</div>
</div>

</div>
    </div>
  </div>
</body>

 


</html>"

## Sampling of strong orientations

# Teaching

From August 2017 to December 2018 I was a TA for
[CS1371](https://cs1371.gatech.edu) at Georgia Tech.

# Personal
