# SPCN-011
**สร้าง vm and ct on Proxmox cluster**
# 1. **create master vm (ubuntu-22.04)**
* คลิกที่ create VM!
![image](https://user-images.githubusercontent.com/119166253/208306779-ec3f19b4-c2ba-4e4c-9f97-6ec2a1f25a98.png)

* ตั้งชื่อ VM

![image](https://user-images.githubusercontent.com/119166253/208306875-e8f32974-61bc-42fe-9744-66f2fc06fc70.png)
* เมื่อcreate VM!เสร็จจะได้ ดังรูป

![image](https://user-images.githubusercontent.com/119166253/208306972-b3054633-32bf-4292-b5e3-150afdc99ca6.png)
* master VM import SSH identity from Github

![image](https://user-images.githubusercontent.com/119166253/208308310-af374d8b-5c4b-447f-83cd-bb984789d067.png)
* clone master vm to tamplate

คลิกขวาที่ VM และเลือก Convert to template

![image](https://user-images.githubusercontent.com/119166253/208310097-3fee5812-bafc-42c1-8456-994810aa7063.png)


จะได้ตัว VM เป็นแบบ template

![image](https://user-images.githubusercontent.com/119166253/208309664-6f7672d5-cf3b-496b-976d-6f0b6893a269.png)

* clone from template สร้าง vm ใหม่จำนวน 2 ตัว

คลิกขวาที่ template และเลือก clone

![image](https://user-images.githubusercontent.com/119166253/208309836-d76f2a7f-5eae-47af-803e-fc610b28b925.png)

ตั้งชื่อ VM ที่เรา clone ออกมาทั้ง 2 ตัว

![image](https://user-images.githubusercontent.com/119166253/208308541-1be64b92-d354-43ea-bac7-f252cbd5f90a.png)

**คำสั่งในการ change host name**

            sudo hostnamectl set-hostname [ชื่อที่ต้องการเปลี่ยน]
            
**คำสั่งในการ Set Time**

             date                                            //เอาไว้เพื่อเช็ค local time ปัจจุบัน
             sudo timedatectl set-timezone Asia/Bangkok      //เปลี่ยน timezone ให้เป็น Bangkok
                  
**คำสั่งเกี่ยวกับ QEMU Guest Agent**

            sudo apt install qemu-guest-agent               //ติดตั้ง QEMU Guest Agent
            sudo systemctl start qemu-guest-agent           //เปิดใช้ QEMU Guest Agent
            sudo systemctl status qemu-guest-agent          //เช็คสถานะของ QEMU Guest Agent 
            
**คำสั่งที่ใช้เปลี่ยน IP ของ VM ที่ clone มาทั้ง 2 ตัวเพื่อให้ IP ของ VM ไม่ซ้ำกัน**

            sudo -i                                           ///root
            rm /var/lib/dbus/machine-id     
            nano /etc/machine-id                              //ลบข้อมูลทั้งหมดใน machine-id
            ln -s /etc/machine-id /var/lib/dbus/machine-id    //link ข้อมูลในไฟล์ machine-id
            reboot                                            //เพื่อให้ระบบ reboot
            
 clone ตัวแรก (IP คือ 172.31.1.156)    
 
![image](https://user-images.githubusercontent.com/119166253/208310524-668117f2-c59e-4fbe-a6e5-9cd3a873ff95.png)

clone ตัวแรก (IP คือ 172.31.1.161)

![image](https://user-images.githubusercontent.com/119166253/208310601-b63032b5-21c5-43b1-bc77-17ed40738399.png)

# **2. create vm from other os**

* คลิกที่ create VM และตั้งชื่อเป็น nattiya-otheros-234

![image](https://user-images.githubusercontent.com/119166253/208310748-5d9548f6-4e17-4e3a-8f66-95f08dbf7e64.png)

* เลือก os kali-linux-2022.4-live-amd64.iso

![image](https://user-images.githubusercontent.com/119166253/208310871-6603ac30-117b-4efb-85d8-311cab630010.png)

* เปลี่ยน timezone ให้เป็น Bangkok

* เปิดใช้งาน QEMU Guest Agent

* คำสั่งในการเปิดใช้งาน Qemu Guest Agent

            apt update && apt -y install qemu-guest-agent 
            systemctl enable qemu-guest-agent 
            systemctl start qemu-guest-agent 
            systemctl status qemu-guest-agent
            
![image](https://user-images.githubusercontent.com/119166253/208311197-c2e08821-6513-4aad-8154-91c5fe1d7131.png)

![image](https://user-images.githubusercontent.com/119166253/208311255-4a305c91-47a4-4c74-8d06-ed4bffaeb00a.png)

# 3.create container template (select from CT list)

* คลิกที่ Create CT

![image](https://user-images.githubusercontent.com/119166253/208311390-54b13d71-f334-4d68-878d-989d1dc09394.png)

* ตั้งชื่อ ใส่รหัสและ LOAD SSH Public Key File

![image](https://user-images.githubusercontent.com/119166253/208311440-e03ae7ba-f779-4a1d-9b6b-ff28d6cf6b8c.png)

* เลือก Template

![image](https://user-images.githubusercontent.com/119166253/208311525-bfddd187-2492-4e48-a6ad-438139cfd440.png)

* เลือก Disk

![image](https://user-images.githubusercontent.com/119166253/208311580-1d975632-e63b-4eea-9aff-a61de6481648.png)

* เลือก Cpu

![image](https://user-images.githubusercontent.com/119166253/208311612-872b9ca2-a7ad-4ae3-ba33-dfb65cebe452.png)

* เลือก memory

![image](https://user-images.githubusercontent.com/119166253/208311651-8ed330ae-c301-48c8-bc75-3362471e39bf.png)

* เลือก IPv4 เป็น DHCP และ IPv6 เป็น SLAAC 

![image](https://user-images.githubusercontent.com/119166253/208311728-3ecd4e81-fed4-4602-81b5-bd0ce03a980e.png)

* เสร็จสิ้น

![image](https://user-images.githubusercontent.com/119166253/208312540-d46612b8-bc52-4be1-bca8-953d21eae35f.png)

![image](https://user-images.githubusercontent.com/119166253/208312599-d1eaa053-677d-41f4-a293-a30bf80bc8d4.png)




            

      
      
