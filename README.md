# conda-recipes

https://anaconda.org/roccqqck 


可安裝在虛擬環境
```
conda install git patch conda-build anaconda-client
conda config --append channels conda-forge
conda skeleton pypi 套件名
```
例如
```
conda skeleton pypi pandas
conda skeleton pypi pandas --version=0.25.3
```
會產生一個套件名資料夾

如果是純python套件 建議用noarch 所有版本皆適用 需有source code

```cd 套件名```
編輯
```vim meta.yaml```

加一行
```
build:
  noarch: python
```

```
cd ~
conda-build 套件名 
```


若沒有source code只有wheel

```cd 套件名```
編輯
```vim meta.yaml```

改source 跟 script
```
source: 
   url: https://files.pythonhosted.org/packages/e8/cf/7089b87fdae8f47be81ce8e2e6377b321805c4648f2eb12fbd2987388dac/sentencepiece-0.1.83-cp37-cp37m-manylinux1_x86_64.whl

script:
    - python -m pip install --no-deps --ignore-installed ./sentencepiece-0.1.83-cp37-cp37m-manylinux1_x86_64.whl
```

```
cd ~
conda-build --python 3.7 套件名
conda-build --python 3.6 套件名
```


上傳到anaconda
```
cd ~/anaconda3/conda-bld/noarch
anaconda upload 套件名.tar.bz2
```
輸入anaconda的帳號密碼