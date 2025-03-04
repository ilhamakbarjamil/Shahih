# 1. Siapkan virtual machine/PC dan masuk sebagai user praktikum2025
id

# 2. Pindah ke user root menggunakan sudo
sudo -i

# 3. Buat user baru bernama student dan pastikan home directory terbuat
sudo useradd -m student
getent passwd student

# 4. Set password user student menjadi StUd3nT!23
echo "StUd3nT!23" | sudo passwd --stdin student

# 5. Buat user informatic, faculty, cloudadmin, dan serveradmin
sudo useradd -m informatic
sudo useradd -m faculty
sudo useradd -m cloudadmin
sudo useradd -m serveradmin

# Set password user menjadi t3chN0logy
echo "t3chN0logy" | sudo passwd --stdin informatic
echo "t3chN0logy" | sudo passwd --stdin faculty
echo "t3chN0logy" | sudo passwd --stdin cloudadmin
echo "t3chN0logy" | sudo passwd --stdin serveradmin

# 6. Update akun user cloudadmin dan serveradmin dengan comment
sudo usermod -c "Cloud Administrator" cloudadmin
sudo usermod -c "Server Administrator" serveradmin

# Verifikasi
getent passwd cloudadmin
getent passwd serveradmin

# 7. Hapus user cloudadmin dan informatic beserta home directory
sudo userdel -r cloudadmin
sudo userdel -r informatic

# Verifikasi
getent passwd cloudadmin informatic

# 8. Buat grup administration dengan GID 30000 dan temporary dengan range sistem
sudo groupadd -g 30000 administration
sudo groupadd -r temporary

# Verifikasi
getent group administration
getent group temporary

# 9. Tambahkan faculty dan serveradmin ke grup administration
sudo usermod -aG administration faculty
sudo usermod -aG administration serveradmin

# Aktifkan hak administratif untuk grup administration
sudo visudo
# Tambahkan baris berikut di dalam file visudo:
# %administration ALL=(ALL) ALL

# 10. Hapus grup temporary dan ubah GID grup administration ke 22000
sudo groupdel temporary
sudo groupmod -g 22000 administration

# 11. Pindah ke user faculty dan lakukan tugas
su - faculty
sudo head -n 10 /var/log/dnf.log
sudo cp /etc/issue /etc/issueBACKUP
sudo rm /etc/issueBACKUP

# 12. Pindah ke user serveradmin dan tampilkan informasi
su - serveradmin
whoami
groups
pwd
echo $HOME
echo $SHELL
echo $PATH

# 13. Pindah ke root dengan non-login shell
sudo bash
whoami
groups
pwd
echo $HOME
echo $SHELL
echo $PATH

# 14. Pindah ke root dengan login shell
sudo -i
whoami
groups
pwd
echo $HOME
echo $SHELL
echo $PATH
