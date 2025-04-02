# Profile Project
This is Website for Practicum in Software Development course, I over done it a bit take much longer than I expect
The code in ProfileView.vue is very VERY VERY messy, I know I should separate more element.But it work fine and half of it is just CSS, and almost other half is DB related so shouldn't be hard to read (surely).

## Requirements
### แสดงข้อมูลนิสิต 
- รูปภาพตัวเองเท่านั้น (เห็นหน้าจะได้รู้ว่าใคร) 2++ ✅ 3 picture, I usally not take picture so not much to give here.  
- ชื่อ-นามสกุล รหัส สาขา ✅ At the home page,first thing you see actually.
- โรงเรียนเดิม ✅ Also at the home page, scroll down. The button redirect you to my old school website  
- แก้ไขข้อมูลได้  
  - ต้องมี Form สำหรับแก้ไข  ✅ Edit button for profile is at bottom right of the first section at home page (You can't edit the old school tho. that would be too complicate)

### แสดงรายละเอียดการเรียน
- รหัสวิชา ชื่อวิชา หน่วยกิต เกรด ✅ At the profile page in card form, it in year card container. Course card met all the requirement. For code it in CourseCard.vue in component  
- เพิ่ม ลบ แก้ไข ได้ ✅ also all in the profile page and course card  
- ต้องมี Form สำหรับเพิ่มและแก้ไข ✅ and also in the card it self  

Note: I also store year and colour of the course.So it a bit more complicated

### การพัฒนา Application
- ใช้ Vue.js ✅ all use vue but I set up the vue wrong a bit so there will be some ts element left in not effect the code, I not even use it (ts).  
- json-server (data/db.json) ✅ db.json in data, it contain course with all element, year, the setting for the year and profile data.

- เอาไปไว้ที่ GitHub ของแต่ละคน ✅  
- ตั้งชื่อ repository → project214_รหัสนิสิต เช่น project214_6630209988 ✅  

### ตบแต่งตามที่เรียนมา 
- HTML, CSS, CSS Framework (Bootstrap) ✅ alot css is used and I mean ALOT, but I didnt use Boostrap, it not my style.  
- ถ้าเหมือนกันจนรู้สึกได้ แบ่งคะแนนตามจำนวนคนที่เหมือน ✅ well there a friend that also use the SpaceX sytle like me but pretty sure other thing is not even close  
  - เช่น การจัดวางเหมือนกัน เปลี่ยนแต่ข้อมูล, Font, Background ชิดซ้าย ชิดขวา  
  - ต้นฉบับควรจะมีหลาย Version เพราะไม่รู้ใครเป็นต้นฉบับ → แบ่งเท่าๆกัน  
- ส่งได้ตั้งแต่วัน 08 มีนาคม 2568 - วันที่ 4 เมษายน 2568 ส่งเลยเวลามีผลต่อคะแนน ✅ Submited! at 00:49 Thursday, April 3, 2025 (GMT+7) !!!

## Project Setup

```sh
npm install
npm install json-server
```

### Run project

```sh
npm run dev
```
### Connect db

```sh
npx json-server --watch data/db.json
```
