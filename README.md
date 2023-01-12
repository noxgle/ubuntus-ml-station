# ml-station
Ubuntu machine-learning-station with NVIDIA gpu.

## Steps
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
7. Get jupter token, in container console:
```
cat nohup.out
```
Open your internet browser: 
```
http://your-ip-address:8888/?token=your-token
```

# Optional
You can install "portainer" if you want graphical access to docker:
```
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```
Open your internet browser:
```
https://your-ip-address:9443
```
