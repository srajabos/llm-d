**Start docker **

docker run -td --rm --privileged --net=host --device=/dev/dri  --name=xpu-llmd-container -v $HOME:/apps  -e no_proxy=localhost,127.0.0.1 -e http_proxy=$http_proxy  -e https_proxy=$https_proxy     --shm-size="32g"     --entrypoint /bin/bash    ghcr.io/llm-d/llm-d-xpu:v0.3.1

docker exec -it xpu-llmd-container bash

**Inside the docker**

cd /workspace/
export NIXL_VERSION=0.7.0
python /workspace/vllm/tools/install_nixl_from_source_ubuntu.py --force-reinstall

Get the updated run_accuracy_test.sh and toy_proxy.py from [here](https://github.com/srajabos/llm-d/tree/xpu-pd/xpu-pd)

cd /workspace/llm-d/xpu-md
bash run_accuracy_test.sh
