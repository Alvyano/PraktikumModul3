# Praktikum Modul 3

# Study Case

```
Kelompok 9 : 
1. Difa Taufiqurahman 1202199005
2. Alvyano Rizqilla 1202190035
```

 - The first step is to go to the directory using ansible
 
![](Praktikum3/1.PNG)

![](Praktikum3/2.PNG)

```
 ---
- hosts: all
  become : yes
  tasks:
    - name: install bind9 dan dnsutils
      apt:
       pkg:
         - bind9
         - dnsutils
```

- After going to the laravel.yml web directory. The next step is to re-install

![](Praktikum3/3.PNG)

- Then Create a file e config1.yml

![](Praktikum3/4.PNG)

```
 ---
- hosts: all
  become : yes
  tasks:
   - name: membuat direktori
     file:
      path: /var/www/html/dev/landing
      state: directory
   - name: copy file vm.local
     copy:
      src: /etc/bind/vm/vm.local
      dest: /var/www/html/dev/landing
   - name: mengganti konfigurasi
     replace:
      path: /var/www/html/dev/landing/vm.local
      regexp: 'www'
      replace: 'dev'
   - name: copy file named.conf.local
     copy:
      src: /etc/bind/named.conf.local
      dest: /etc/bind/named.conf.local
   - name: mengganti konfigurasi conf local
     replace:
      path: /etc/bind/named.conf.local
      regexp: '/etc/bind/vm/vm.local'
      replace: '/var/www/html/dev/landing/vm.local'
   - name: mengganti konfigurasi conf local part2
     replace:
      path: /etc/bind/named.conf.local
      regexp: '/etc/bind/vm/1.168.192.in-addr.arpa'
      replace: '/var/www/html/dev/landing/1.168.192.in-addr.arpa'
   - name: copy file 1.168.192.in-addr.arpa
     copy:
      src: /etc/bind/vm/1.168.192.in-addr.arpa
      dest: /var/www/html/dev/landing
   - name: copy file resolv.conf
     copy:
      src: /etc/resolv.conf
      dest: /etc/resolv.conf
   - name: copy file named.conf.options
     copy:
      src: /etc/bind/named.conf.options
      dest: /etc/bind/named.conf.options
   - name: restart nginx
     service:
      name: nginx
      state: restarted
   - name: restart bind9
     action: service name=bind9 state=restarted
```

- Perform the installation using the command and script below

![](Praktikum3/5.PNG)

- Add subdomain to /etc/hosts

![](Praktikum3/6.PNG)

- Then open the vm.local file

![](Praktikum3/7.PNG)

- Add the www line to the vm.local file

![](Praktikum3/8.PNG)

- The final step is to exit and the web will appear in vm.local/

![](Praktikum3/9.PNG)

- Open and edit vm.local in directory /etc/nginx/sites-enabled/

![10](https://user-images.githubusercontent.com/80197844/146380068-2e8dafd0-296d-4622-9e44-8f1b4b52c430.PNG)

- Edit vm.local add "dev.www.vm.local;"

![11](https://user-images.githubusercontent.com/80197844/146380174-bb74e16e-b0a7-4b27-95da-2ba549b3fea8.PNG)

- Open and edit vm.local in directory /etc/bind/vm/

![12](https://user-images.githubusercontent.com/80197844/146380489-d0c2673c-23a6-4f04-a9fc-9abe2454d9e1.PNG)

- Restart all packages

![13](https://user-images.githubusercontent.com/80197844/146380650-e4965b80-398a-4545-abe1-2d019108baff.PNG)

- Open Change Adaptor Settings (in the case we use Windows and LAN) thats why we choosed ethernet not WiFi. uncheck internet protocol version (TCP/IPv6)

![14](https://user-images.githubusercontent.com/80197844/146380726-cf15d7a4-d9f6-4e91-ae33-857b8734693d.PNG)

- Open internet protocol version (TCP/IPv4) properties, change DNS with ip like a image

![15](https://user-images.githubusercontent.com/80197844/146381010-3ca11b8a-07de-49cb-83e4-1fce9f8228f6.PNG)

- and check vm.local/ in the browser

![](Praktikum3/10.PNG)


