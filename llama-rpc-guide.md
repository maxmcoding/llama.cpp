

UBUNTU CENTRAl HOST



sudo apt install -y git cmake build-essential libvulkan-dev vulkan-tools
sudo apt update && sudo apt install -y vulkan-tools glslang-tools
sudo apt update && sudo apt install -y glslc vulkan-tools  spirv-headers


git clone https://github.com/ggml-org/llama.cpp.git
cd llama.cpp

cmake -B build -DGGML_VULKAN=ON -DGGML_RPC=ON -DCMAKE_BUILD_TYPE=Release
cmake --build build --config Release --parallel

** Server Central
./build/bin/llama-cli  -hf lmstudio-community/Qwen3.5-9B-GGUF -ngl 99  --rpc [TARGET_IP]:50052,[TARGET_IP_2.xxx]:50052

///adicional parametros 
   -kvo  -fa on  --temp 1  --top-k 20  --top-p 0.95  --repeat-penalty 1.15  --presence-penalty 0.1



--------------------------------------------------
BC-250


sudo dnf install -y git gcc make

git clone https://github.com/fanoush/bc250_memcfg
cd bc250_memcfg && make
# Force 10GB Allocation to the GPU (leaving 6GB for OS/Inference overhead)
sudo ./bc250memcfg UMA_SIZE 10240
sudo reboot


sudo dnf install -y git cmake gcc-c++ vulkan-loader-devel mesa-vulkan-drivers vulkan-tools glslc glslang 


git clone https://github.com/ggml-org/llama.cpp.git
cd llama.cpp
cmake -B build -DGGML_VULKAN=ON -DGGML_RPC=ON -DCMAKE_BUILD_TYPE=Release
cmake --build build --config Release --parallel

** Expose device
./build/bin/ggml-rpc-server --host 0.0.0.0 --port 50052
