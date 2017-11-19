# BlinkDL

A minimalist deep learning library in Javascript using WebGL + asm.js. Runs in your browser. 

Currently it is a proof-of-concept (inference only).

## Example

A weiqi (baduk, go) policy network in AlphaGo style:

    const N = 19;
    const NN = N * N;
    const nFeaturePlane = 8;
    const nFilter = 128;

    const x = new BlinkArray();
    x.Init('weblas'); // WebGL backend, from https://github.com/waylonflinn/weblas
    x.nChannel = nFeaturePlane;
    x.data = new Float32Array(nFeaturePlane * NN);
    
    // pre-act residual network with 6 residual blocks
    const bak = new Float32Array(nFilter * NN);
    x.Convolution(nFilter, 3);
    x.CopyTo(bak);
    x.BatchNorm().ReLU().Convolution(nFilter, 3);
    x.BatchNorm().ReLU().Convolution(nFilter, 3);
    x.Add(bak).CopyTo(bak);
    x.BatchNorm().ReLU().Convolution(nFilter, 3);
    x.BatchNorm().ReLU().Convolution(nFilter, 3);
    x.Add(bak).CopyTo(bak);
    x.BatchNorm().ReLU().Convolution(nFilter, 3);
    x.BatchNorm().ReLU().Convolution(nFilter, 3);
    x.Add(bak).CopyTo(bak);
    x.BatchNorm().ReLU().Convolution(nFilter, 3);
    x.BatchNorm().ReLU().Convolution(nFilter, 3);
    x.Add(bak).CopyTo(bak);
    x.BatchNorm().ReLU().Convolution(nFilter, 3);
    x.BatchNorm().ReLU().Convolution(nFilter, 3);
    x.Add(bak).CopyTo(bak);
    x.BatchNorm().ReLU().Convolution(nFilter, 3);
    x.BatchNorm().ReLU().Convolution(nFilter, 3);
    x.Add(bak);
    x.BatchNorm().ReLU().Convolution(1, 1).Softmax();
    
## Usage

    <script src='weblas.js' type='text/javascript'></script>
    <script src='BlinkDL.js' type='text/javascript'></script>
 
