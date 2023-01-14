# ml-station
Ubuntu machine-learning-station with NVIDIA gpu.

# Step 1: Get and install Ubuntu 20.04 (minimal install)
# Step 2: Update, upgrade, and install necessary packages
```
sudo apt update && apt -y upgrade && apt install ssh, screen, git 
git clone https://github.com/NVIDIA/data-science-stack
cd data-science-stack
./data-science-stack setup-system
```
# Step 3: Check if Nvidia GPU is working
```
nvidia-smi
```
if no, then:
```
./data-science-stack install-driver
reboot
./data-science-stack setup-system
reboot
```
# Step 4: Create a "workspace" folder in the user directory
mkdir ~/workspace
# Step 5: Run Docker container with necessary options
```
docker run  -t -i -v /home/user/workspace:/workspace --restart always -p 8888:8888 --gpus all -it nvcr.io/nvidia/pytorch:22.12-py3
```
# Step 6: Auto start Jupyter on reboot
```
echo "nohup jupyter-notebook --ip 0.0.0.0 --no-browser --allow-root --port=8888 &" > /opt/nvidia/entrypoint.d/80-jupter.sh
```
# Step 7: Get Jupyter token
```
cat nohup.out
```
Open your internet browser: 
```
http://your-ip-address:8888/?token=your-token
```
# Optional: Install Portainer for graphical access to Docker
```
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```
Open your internet browser:
```
https://your-ip-address:9443
```
