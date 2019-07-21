function readModel(YourModelName, targetSize = 60) {

    var onProgress = function(xhr) {
      if (xhr.lengthComputable) {
        var percentComplete = xhr.loaded / xhr.total * 100;
        console.log(Math.round(percenyComplete, 2) + '% downloaded')
      }

    };
    var onError = function(xhr) {
      console.log("error")
    };
    var mtlLoader = new THREE.MTLLoader();
    mtlLoader.setPath('https://cdn.jsdelivr.net/gh/RGMGx/RGMGx.github.io@87d437256b55c6cea59810e522ac8969e92770ca/models/');

    mtlLoader.load('YourModelName.mtl', function(materials) {
      materials.preload();
      var objLoader = new THREE.OBJLoader();
      objLoader.setMaterials(materials);
      objLoader.setPath('https://cdn.jsdelivr.net/gh/RGMGx/RGMGx.github.io@87d437256b55c6cea59810e522ac8969e92770ca/models/')
      objLoader.load('YourModelName.obj', function(object) {
        let theObject = unitize(object, targetSize);
        // theObject.add(new THREE.BoxHelper(theObject))
        theObject.name = 'OBJ';

        scene.add(theObject)
      }, onProgress, onError);
    });
  }
  readModel();
  