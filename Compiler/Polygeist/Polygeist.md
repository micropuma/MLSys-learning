# Polygeist 
## Overall Stucture 
![](../../png/polystructure.png)  
The Whole project can be divided into three components:  
* C/C++ to MLIR IR front end part
* raise-affine to **PolyhedralModel** and then lower-affine to mlir-scf IR part, which is the **core part** of the whole pipeline. 
* codegen to llvm-ir and to binary(Cuda is optional).  

### Main features  
The most outstanding feature is the reuse of existing mature and state of art infrastructure.  
* In front end：**Polygeist leverages Clang infrastructure to perform syntactic
and semantic analysis of the input code.** Conver c/c++ code to MLIR SCF dialect or standard dialect. Turn to original essay for more details about the thorough pipeline of the front end and process of Local Variables or things like that.
* In Middle end, First part is **Generating Affine Code**.  Then what Polygeist did is to use existing Polyhedral compilation part such as Pluto. So we shoulld lower dialect to **OpenScop (Used by Pluto and many others!)**, and then back to mlir. 
* In backend, we simply reuse mlir framework to lower the code to whatever backend we wish! MLIR IR is fabulous!

## Reproduce the paper
### Run cgeist
```shell
./cgeist gemm.c -function=matmul -raise-scf-to-affine -S
```


## References 
1. [Polygeist论文](https://ieeexplore.ieee.org/document/9563011)
2. [Affine Dialect官方文档](https://mlir.llvm.org/docs/Dialects/Affine/)
3. [Linalg Dialect官方文档](https://mlir.llvm.org/docs/Dialects/Linalg/)
