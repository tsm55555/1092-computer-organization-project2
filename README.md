# 1092-computer-organization-project2
### GEM5

scons EXTRAS=../NVmain build/X86/gem5.opt


## ✅ 1. GEM5 + NVMAIN BUILD-UP (40%)

### Implementation
跟著講義做

./build/X86/gem5.opt configs/example/se.py -c tests/test-progs/hello/bin/x86/linux/hello --cpu-type=TimingSimpleCPU --caches --l2cache --mem-type=NVMainMemory --nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config

## ✅ 2. Enable L3 last level cache in GEM5 + NVMAIN (15%)

### Implementation
參考:https://blog.csdn.net/tristan_tian/article/details/79851063?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-4.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-4.control

照講義添加LL3cache 的參數

recompile gem5 (scons EXTRAS=../NVmain build/X86/gem5.opt)

./build/X86/gem5.opt configs/example/se.py -c tests/test-progs/hello/bin/x86/linux/hello --cpu-type=TimingSimpleCPU --caches --l2cache --l3cache --mem-type=NVMainMemory --nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config

## ✅ 3. Config last level cache to 2-way and full-way associative cache and test performance (15%)

### 2-way
./build/X86/gem5.opt configs/example/se.py -c ./benchmark/quicksort --cpu-type=TimingSimpleCPU --caches --l2cache --l3cache --l3_assoc=2 --l1i_size=32kB --l1d_size=32kB --l2_size=128kB --l3_size=1MB --mem-type=NVMainMemory --nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config

system.l3.overall_miss_rate::total           0.539978                   


### full-way
./build/X86/gem5.opt configs/example/se.py -c ./benchmark/quicksort --cpu-type=TimingSimpleCPU --caches --l2cache --l3cache --l3_assoc=16384 --l1i_size=32kB --l1d_size=32kB --l2_size=128kB --l3_size=1MB --mem-type=NVMainMemory --nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config

system.l3.overall_miss_rate::total           0.741649 

## ✅ 4. Modify last level cache policy based on RRIP (15%)
助教現場給code

compile: gcc --static FileName.c -o OutputName

./build/X86/gem5.opt configs/example/se.py -c ./OutputName --cpu-type=TimingSimpleCPU --caches --l2cache --l3cache --l1i_size=32kB --l1d_size=32kB --l2_size=128kB --l3_size=1MB --mem-type=NVMainMemory --nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config

## 🔳 5. Test the performance of write back and write through policy based on 4-way associative cache with isscc_pcm(15%)
todo

![image](https://i.giphy.com/media/QmJ3e9So5M9NdNkOGo/giphy.webp)

![image](https://media2.giphy.com/media/sS8YbjrTzu4KI/giphy.gif?cid=790b761153b8ea69f141ec6195014a1a3eb9323ed261acfd&rid=giphy.gif&ct=g)

./build/X86/gem5.opt configs/example/se.py -c ./benchmark/multipy --cpu-type=TimingSimpleCPU --caches --l2cache --l3cache --l3_assoc=4  --l1i_size=32kB --l1d_size=32kB --l2_size=128kB --l3_size=1MB --mem-type=NVMainMemory --nvmain-config=../NVmain/Config/PCM_ISSCC_2012_4GB.config
## 🔳 Bonus (20%)
Design last level cache policy to reduce the energy consumption of pcm_based main memory

Baseline:LRU

![image](https://i.imgur.com/YnDdljo.gif)

