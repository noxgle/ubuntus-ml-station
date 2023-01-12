# ml-station
Machine-learning-station with NVIDIA gpu.

# Install
1. Get and install ubuntu 20.04 - choose minimal install
2. In terminal in home user directory:
```
sudo apt update && apt -y upgrade && apt install ssh, screen, git 
git clone https://github.com/NVIDIA/data-science-stack
cd data-science-stack
./data-science-stack setup-system
```
3. Check if we have working Nvidia gpu:
```
nvidia-smi
```
if no then:
```
./data-science-stack install-driver
reboot
./data-science-stack setup-system
reboot
```
4. Create foder "workspace" in user directory.
5. Docker:
```
docker run  -t -i -v /home/user/workspace:/workspace --restart always -p 8888:8888 --gpus all -it nvcr.io/nvidia/pytorch:22.12-py3
```
6. Jupyter start on reboot container:
```
echo "nohup jupyter-notebook --ip 0.0.0.0 --no-browser --allow-root --port=8888 &" > /opt/nvidia/entrypoint.d/80-jupter.sh
```
