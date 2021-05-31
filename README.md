# Ubuntu-Speedup

sudo ufw logging off

sudo apt-get purge mlocate locate

xed admin:///etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
[connection]
wifi.powersave = 2

sudo cp -v /usr/share/systemd/tmp.mount /etc/systemd/system/
sudo systemctl enable tmp.mount
reboot
systemctl status tmp.mount

xed admin:///etc/default/grub
GRUB_CMDLINE_LINUX="zswap.max_pool_percent=40"
sudo update-grub
reboot
cat /sys/module/zswap/parameters/max_pool_percent

xed admin:///etc/sysctl.conf
vm.vfs_cache_pressure=50


sudo mkdir -v /etc/systemd/system/fstrim.timer.d
sudo touch /etc/systemd/system/fstrim.timer.d/override.conf
xed admin:///etc/systemd/system/fstrim.timer.d/override.conf
[Timer]
OnCalendar=
OnCalendar=daily
reboot
systemctl cat fstrim.timer

#Firefox
about:config
browser.cache.disk.enable		(disable)
browser.cache.memory.enable		(enable)
browser.cache.memory.capacity 	(524288)

#Chrome
Settings
Privacy and security
Cookies and site data
Preload pages for faster browsing and searching (disable)

cat /sys/block/sda/queue/scheduler
xed admin:///etc/default/grub
GRUB_CMDLINE_LINUX_DEFAULT="elevator=noop quiet splash zswap.max_pool_percent=40"
sudo update-grub

sudo sed -i 's/ errors=remount-ro/ noatime,errors=remount-ro/' /etc/fstab
sudo sed -i 's/ defaults/ noatime,defaults/' /etc/fstab

sudo apt-get remove "fonts-kacst*" "fonts-khmeros*" fonts-lklug-sinhala fonts-guru-extra "fonts-nanum*" fonts-noto-cjk "fonts-takao*" fonts-tibetan-machine fonts-lao fonts-sil-padauk fonts-sil-abyssinica "fonts-tlwg-*" "fonts-lohit-*" fonts-beng-extra fonts-gargi fonts-gubbi fonts-gujr-extra fonts-kalapi "fonts-samyak*" fonts-navilu fonts-nakula fonts-orya-extra fonts-pagul fonts-sarai "fonts-telu*" "fonts-wqy*" "fonts-smc*" fonts-deva-extra fonts-sahadeva
sudo dpkg-reconfigure fontconfig

sudo journalctl --vacuum-size=50M
sudo sed -i 's/#SystemMaxFiles=100/SystemMaxFiles=7/g' /etc/systemd/journald.conf

sudo rm -v /var/log/*.log* /var/log/syslog*
sudo sed -i 's/rotate 7/rotate 1/g' /etc/logrotate.d/rsyslog
sudo sed -i 's/rotate 4/rotate 1/g' /etc/logrotate.d/rsyslog
sudo sed -i 's/weekly/daily/g' /etc/logrotate.d/rsyslog
sudo sed -i 's/rotate 4/rotate 1/g' /etc/logrotate.conf
sudo sed -i 's/weekly/daily/g' /etc/logrotate.conf
reboot

