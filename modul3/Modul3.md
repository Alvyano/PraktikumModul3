# Praktikum Modul 3

# Study Case


 - The first step is to go to the directory using ansible
 
![](PraktikumModul3/1.png)

![](Praktikum3/2.PNG)

- After going to the laravel.yml web directory. The next step is to re-install

![](Praktikum3/3.PNG)

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

- Then Create a file e config.yml

![](Praktikum3/4.PNG)

- Perform the installation using the command and script below

![](Praktikum3/5.PNG)

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
      regexp: '/etc/bind/vm/115.168.192.in-addr.arpa'
      replace: '/var/www/html/dev/landing/115.168.192.in-addr.arpa'
   - name: copy file 115.168.192.in-addr.arpa
     copy:
      src: /etc/bind/vm/115.168.192.in-addr.arpa
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

- Add subdomain to /etc/hosts

![](Praktikum3/6.PNG)

- Then open the vm.local file

![](Praktikum3/7.PNG)

- Add the www line to the vm.local file

![](Praktikum3/8.PNG)

- The final step is to exit and the web will appear in vm.local/

![](Praktikum3/9.PNG)

![](Praktikum3/10.PNG)


