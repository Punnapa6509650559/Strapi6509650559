## What is Strapi ?

Strapi คือ โปรแกรม Headless CMS ( Content Management System : CMS) ที่เป็น Open Source ที่พัฒนาด้วย Node.js ซึ่งสามารถนำไปใช้สร้าง API ด้วย Javascript ได้อย่างรวดเร็ว และใช้งานได้ฟรี 

**Objective**
Headless CMS จะแยกการทำงานของ Front-end, Back-end และ Database ออกจากกันเป็นส่วน ๆ ทำให้ Developer สามารถแยกกันทำงานในแต่ละส่วนได้ในเวลาเดียวกัน และมีระบบในการจัดการ spec ของ API ผ่านหน้า Admin Dashboard ซึ่งสามารถทำให้เรา Customize API ให้ตรงกับความต้องการของโปรเจกต์ได้

**Use Cases**

 - Website องค์กร : สร้าง Website สำหรับองค์กรที่สามารถจัดการเนื้อหาได้หลากหลายประเภท 
 - E-commerce : สามารถ Customize ร้านค้าออนไลน์ได้ตั้งแต่การจัดการสินค้า การชำระเงิน และ Tracking การขนส่ง 
 - Blog : สร้าง Website และจัดการเนื้อหาได้อย่างสะดวก

**Component**

Strapi มี Component หลักๆ อยู่ 2 ประเภท

1. Single Types : ใช้เพื่อจัดการเนื้อหาที่มีไม่ซ้ำ เช่น หน้า Homepage, หน้าการตั้งค่าเว็บไซต์ (Site Configuration), หน้า Privacy Policy ซึ่งการสร้าง Single Type สามารถทำได้ผ่าน Content-Type Builder ใน Strapi ได้ โดยเราสามารถเพิ่ม Field พวกรูปภาพ, Text หรืออื่นๆ เพื่อกำหนดโครงสร้างของเนื้อหาได้ตามต้องการ

2. Collection Types : ใช้จัดการเนื้อหาที่มีหลายรายการ เช่น บทความ, ผลิตภัณฑ์, User Profiles, Orders หรือเนื้อหาที่สามารถเพิ่มลบได้ ซี่งการสร้าง Collectiom Types ก็สามารถสร้างและเพิ่ม Field ที่ต้องการได้ผ่าน Content-Type Builder ใน Strapi เช่นกัน

และนอกจากนี้ Strapi ยังมี Dynamic Zones เป็นฟีเจอร์ที่ช่วย Customize หน้าเว็บได้อย่างรวดเร็ว และช่วยลดเวลาที่ Developers ต้องใช้ในการเพิ่มเนื้อหาใหม่ โดยเราสามารถเพิ่ม Components ต่างๆ ลงใน Content Types ได้ตามต้องการ

**How to install Strapi from CLI**

 สิ่งที่ต้องมีในเครื่องของเรา 

 - Node.js : Currently Version 18 and Version 20
 - Node.js package manager : npm (Version 6 and above), yarn

**Creating a Strapi project**

1. เปิด Terminal และ cd เข้าไปใน Folder ที่ต้องการจัดเก็บโปรเจกต์
2. ใช้คำสั่ง `npx create-strapi-app@latest my-project`ใน Command 

ซึ่งถ้าต้องการใช้ Defualt Database โดยใส่ `--quickstart` ต่อท้าย หรือสามารถ Manual Setting เอง~~ก็ได้
3. หลังจากรันคำสั่งจะมีคำถามขึ้นมาว่าต้องการ login หรือ skip ซึ่งเราสามารถเลือกได้ตามต้องการ (ในการบ้านนี้เลือก skip)
4. เมื่อ Install สำเร็จจะไปที่หน้าเว็บให้เราสร้าง Account
5. เมื่อกรอกข้อมูลเรียบร้อยเราจะสามารถใช้งาน Strapi ได้ โดยเราสามารถเปิดการใช้งาน Strapi ได้ด้วยคำสั่ง `npm run develop`
Ref : 
https://morphos.is/th/blog/what-is-strapi-and-how-it-will-dominate-the-world-of-headless-cms
https://strapi.io/features/content-types-builder
https://docs.strapi.io/dev-docs/installation/cli
## .gitignore
.gitignore เป็นไฟล์ที่บอก git ว่าไม่ให้ Track หรือสนใจ File หรือ Directory ไหนในโปรเจกต์บ้างเมื่อเรา Push หรือ Commit ขึ้น Repository และเมื่อคนอื่น Clone Repositoty ของเราไป จะไม่ได้ File ที่อยู่ในลิสต์ใน .gitignore ของเรา (อาจจะเป็น File ที่ Concern เรื่อง Privacy เช่น Key API เป็นต้น)
ref : 
https://docs.github.com/en/get-started/getting-started-with-git/ignoring-files
## Deployment Strapi
**Setup AWS**
เข้าไป Launch EC2 Instances on AWS และ Set ค่า ดังนี้
 - **Instance Type** : t2.medium
 
 - **Security Group**
        - **Type** : HTTPS , **Protocol** : TCP,  **Port range** : 443,  **Source** : 0.0.0.0/0
        -  **Type**   : Custom TCP Rule ,  **Protocol**  : TCP,  **Port Range** : 1337,  
        **Source** :  0.0.0.0/0
        - **Type** : SSH , **Protocol** : TCP,  **Port range** : 22,  **Source** :  0.0.0.0/0
        - **Type** : HTTP , **Protocol** : TCP,  **Port range** : 80,  **Source** :  0.0.0.0/0
หลังจากนั้นเชื่อมต่อ Instance ผ่าน SSH Client โดยเปิด Terminal แล้ว cd เข้า Folder ที่เราต้องการ (ภายใน Folder ต้องมีไฟล์ Key Pair ของเรา) หลังจากนั้น copy ค่า SSH ของเราไปรัน
    ssh -i "NewKeyPair.pem" ec2-user@your-instance-public-dns
เมื่อเชื่อมต่อสำเร็จแล้ว อัพเดท Package Manager ด้วยคำสั่ง
    sudo yum update
**Install Node.js และ npm**  ด้วยคำสั่ง
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
    #เพิ่ม NodeSource repositoy
    sudo apt install -y nodejs
    #ติดตั้ง Node.js และ npm
ตรวจสอบการติดตั้ง
    node -v && npm -v
**สร้าง npm global directory**
    cd ~
    mkdir ~/.npm-global #สร้าง directory ใหม่สำหรับ npm global
    npm config set prefix '~/.npm-global'#กำหนด npm ให้ใช้ directory นี้เป็น global directory
**สร้าง Path ไปยัง Environment**
    sudo nano ~/.profile
    export PATH=~/.npm-global/bin:$PATH
    source ~/.profile #ใช้เพื่อให้การเปลี่ยนแปลงที่ทำกับไฟล์ .profile มีผลทันทีโดยที่ไม่ต้องปิด Terminal 
**Install Git** (ถ้าไม่มีในเครื่อง)
    sudo apt install git -y
หลังจากนั้น Clone repository 
    git clone <url git repository>
 cd เข้าโปรเจกต์ที่ Clone มา และใช้คำสั่งต่อไปนี้
 
    npm install #ติดตั้ง library
    NODE_ENV=production npm run build #Build project 
**Install PM2 Runtime**
    npm install pm2 -g
    
**Configure PM2 Runtime**
สร้าง File ecosystem.config.js
    cd ~
    pm2 init
    sudo nano ecosystem.config.js
config โดย set ค่าตาม code นี้
    ```
module.exports = {
  apps: [
    {
      name: 'your-app-name', # Your project name
      cwd: '/home/ubuntu/my-project', #	 Path to your project
      script: 'npm', # หรือใช้ yarn ก็ได้ (แล้วแต่โปรเจกต์เรา)
      args: 'start', 
      env: {
        APP_KEYS: 'your app keys', // ดูได้จากไฟล์ project .env 
        API_TOKEN_SALT: 'your api token salt',
        ADMIN_JWT_SECRET: 'your admin jwt secret', #สามารถ Genarate เองได้
        JWT_SECRET: 'your jwt secret', #สามารถ Genarate เองได้
        NODE_ENV: 'production',
        DATABASE_HOST: 'your-unique-url.rds.amazonaws.com', 
        DATABASE_PORT: '5432',
        DATABASE_NAME: 'strapi', 
        DATABASE_USERNAME: 'postgres',
        DATABASE_PASSWORD: 'Password',
        AWS_ACCESS_KEY_ID: 'aws-access-key-id',
        AWS_ACCESS_SECRET: 'aws-access-secret', 
        AWS_REGION: 'aws-region',
        AWS_BUCKET_NAME: 'my-project-bucket-name',
      },
    },
  ],
};
หลังจากนั้น start ด้วยคำสั่ง
    pm2 start ecosystem.config.js
**รัน PM2**
    pm2 startup systemd
เมื่อรันคำสั่งดังกล่าวจะมีข้อความบน command ให้ copy 
ตัวอย่าง
    sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u your-name --hp /home/your-name
หลังจากนั้น Save PM2
    pm2 save
และสุดท้ายเมื่อเราจะรัน Strapi Project ใช้คำสั่ง 
    npm start
หลังจากนั้นดูว่าเว็บที่เรา deploy รันได้ไหมโดยการใส่ IP address ของ EC2 : Port ที่เรา custom ไว้ (ในโปรเจกต์นี้คือ port range 1337)
ref : https://docs.strapi.io/dev-docs/deployment/amazon-aws
https://copilot.cloud.microsoft/?auth=2 (Prompt : How to deployment Strapi Project to AWS)~~