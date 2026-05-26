khi lo unmount hoac loi share folder PC to vmware
sudo mkdir -p /home/sang/Desktop/work
sudo vmhgfs-fuse .host:/work /home/sang/Desktop/work -o allow_other
