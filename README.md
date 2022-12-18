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






      
      
