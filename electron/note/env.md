https://github.com/Quramy/electron-jsx-babel-boilerplate
はウィンドウズで手順通りコンパイルできた。
しかし、別のファイル（今回の場合three.js）をパイプラインに組み込む方法が分からなかった。
直書きなら当然いけるが、せっかくなのでパッケージ管理したい。

直書きで上手くいっている例だと
https://github.com/jeromeetienne/electron-threejs-example
など色々該当する。

jspmで管理しているプロジェクトもあったが、こちらでは再現できなかった。まだjspmは安定していない印象。

threejsの小さくて動作確認しやすいコードとして下記を用意した。
threejs部分は
http://liginc.co.jp/web/html-css/html/91988
から持ってきた。

```
document.addEventListener('DOMContentLoaded', function() {
    var scene = new THREE.Scene();
    var camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);

    var renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    var geometry = new THREE.CubeGeometry(1,1,1);
    var material = new THREE.MeshBasicMaterial({color: 0x00ff00});
    var cube = new THREE.Mesh(geometry, material);
    scene.add(cube);

    camera.position.z = 5;

    var render = function () {
        requestAnimationFrame(render);

        cube.rotation.x += 0.1;
        cube.rotation.y += 0.1;

        renderer.render(scene, camera);
    };

    render();
});
```

メインとなるhtmlファイルでthree.jsを読み込んでいる必要がある。
メインとなるjsファイルに書き込むと動作しなかった。ファイルを分ける必要がある様子。

#参考
http://qiita.com/Quramy/items/90d61ff37ca1b95a7f6d
