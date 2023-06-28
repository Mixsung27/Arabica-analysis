#**1. Import Data & Python Packages**


1.1 Python Packages ประกอบด้วย
  1. NumPy
  2. Pandas
  3. Matplotlib
  4. Seaborn

1.2 Import data 'arabica_coffee_full_table.csv' ที่ได้มากจาก Kaggle: https://www.kaggle.com/datasets/erwinhmtang/coffee-quality-institute-reviews-may2023?select=arabica_coffee_certification_information.csv
โดยมีข้อมูลทั้งหมด 1509 entries และ ทั้งหมด 42 column ทั้งหมดจะเป็นข้อมูลที่ทางบริษัทผลิตเมล็ดกาแฟต่างๆ ส่งตัวอย่างเมล็ดกาแฟที่ผ่านกระบวนการแปรรูปแล้วมาทำการ Test เพี่อขอใบ Certificate สำหรับแสดงในฉลากผลิตภัณฑ์

# **2.Questioning and hypothesis**

2.2 คำถาม : กระบวนการแปรรูปเมล็ดกาแฟรูปแบบต่าง ๆ   มีผลต่อคะแนนรสสัมผัสและคุณภาพของกาแฟมากไหม  
  
สมมุติฐาน : มีผลค่อนข้างมาก



2.2.1 เริ่มจากการ clean data โดยการดูจำนวนของชุดข้อมูลของ Processing Methods(กระบวนการแปรรูป) กลุ่มต่างๆ ที่มีจำนวนข้อมูลน้อยมากๆ ออกไป เนื่องจากอาจทำให้ผลลัพธ์ที่ได้คลาดเคลื่อน ดังกราฟด้านล่าง

![image](https://github.com/Mixsung27/Arabica-analysis/assets/135399656/e5295c0e-b73f-41bf-9579-8ff57640fb34)


Processing Methods ที่นำมาพิจารณาจะมีดังนี้

1. Washed / Wet
2. Natural / Dry
3. Semi-washed / Semi-pulped
4. Pulp natural / honey
5. Others


2.2.2 พิจารณาอันดับ Processing Methods จากค่าเฉลี่ย Total Cup points(คะแนนรวมที่บ่งบอกคุณภาพของกาแฟ)

เมื่อได้กระบวนการผลิตที่มีข้อมูลมากเพียงพอจะนำมาพิจารณาได้แล้ว ช้คะแนนเฉลี่ย Total cup points ของแต่ละกระบวนการผลิตเป็นเกณฑ์หลักในการบอกคุณภาพของกาแฟ โดยเรียงลำกับจากดีที่สุดไปน้อยสุดดังกราฟด้านล่าง

![image](https://github.com/Mixsung27/Arabica-analysis/assets/135399656/f1433531-5a13-44f0-8a89-421dcff0d10e)

2.2.3 พิจารณา Procesing methods แต่ละแบบ มีคะแนนรสสัมผัสแตกต่างกันในมิติไหนอย่างไร

กราฟ Spider plot ด้านล่างแสดงถึงรสสัมผัสของกาแฟจาก 5 กระบวนการผลิต ซึ่งบอกได้ว่าแต่ละกระบวนการผลิตมีคะแนนรสสัมผัสของกาแฟที่แตกต่างกันมากน้อยแค่ไหน ซึ่งเห็นได้ว่า Pulped natural / honey ที่เป็นกระบวนการผลิตที่ได้ Average total cup points มากที่สุด ได้คะแนนรสสัมผัสมากกว่ากระบวนการผลิตแบบอื่นๆในทุกมิติ ยกเว้นแค่ Balance ที่มีค่าใกล้เคียงกันใน 3 อันดับแรก ส่วนคะแนนรสสัมผัสอื่นๆ ไม่นำมาพิจารณาเพราะมีคะแนนที่มากใกล้เคียงกันจนไม่เห็นความเเตกต่าง

![image](https://github.com/Mixsung27/Arabica-analysis/assets/135399656/8eacb4d4-8cce-4fc6-8fa1-846eed635a2c)

กราฟ Heat map ของคะแนนรสสัมผัสของกาแฟแยกตามกระบวนการผลิต แสดงถึงคะแนนที่มากสีจะยิ่งเข้มขึ้น ซึ่งสังเกตุได้ว่า Pulped natural / honey ที่เป็นกระบวนการผลิตที่ได้ Average total cup points มากที่สุดมีสีที่เข้มกว่ากระบวนการผลิตอื่นๆ ตามลำดับ



2.2.4 พิจารณาโอกาสที่แต่ละ Procesing methods จะสามารถมีคะแนนที่สูงพอที่จะผ่านเป็น Specialty coffee(คือ กาแฟพิเศษ ที่วัดผลตั้งแต่เมล็ดกาแฟจนถึง Process ทุกอย่าง ที่ได้ Total cup points ตั้งแต่ 80 คะแนนเป็นต้นไป) มากน้อยแค่ไหน

![image](https://github.com/Mixsung27/Arabica-analysis/assets/135399656/4b40499b-ea28-45a1-96c3-89a66e5d198f)

โดยกราฟนี้จะแสดงให้เห็นว่ากระบวนการผลิตกาแฟที่แตกต่างกันนั้นมีผลต่อคะแนนรสสัมผัสของกาแฟค่อนข้างมากเลยทีเดียว โดยข้อมูลที่บอกสัดส่วนกระบวนการแปรรูปกาแฟที่ได้ Total cup points มากกว่าเท่ากับ 80 คะแนน เรียกว่า Specialty coffee และน้อยกว่า 80 คะแนน เรียกว่า Non-Specialty coffee บ่งบอกถึงโอกาสที่กาแฟที่ผ่านกระบวนการผลิตนั้นๆ สามารถที่จะเป็น Specialty coffee ได้ ถ้าสังเกตที่ Pulped natural / honey ที่เป็นกระบวนการผลิตที่ได้ Average total cup points มากที่สุดนั้น กาแฟทั้งหมดที่ผ่านการผลิตนี้จะสามารถเป็น Specialty coffee ได้ทั้งหมด และส่วนที่มีผลต่อรสชาติของกาแฟไม่แพ้กัน คือ คุณภาพของเมล็ดกาแฟตั้งแต่แหล่งกำเนิด จะเห็นได้จากอันดับประเทศที่มีเมล็ดกาแฟที่ดีที่สุด 5 อันดับแรกนั้น คือ 
1. Ethiopia ที่ผ่านกระบวนการ Washed / Wet 
2. Guatemala ไม่ระบุกระบวนการ
3. Colombia ที่ผ่านกระบวนการ Double Anaerobic Washed 
4. Brazil ที่ผ่านกระบวนการ Natural / Dry 
5. Peru ที่ผ่านกระบวนการ Washed / Wet 


ซึ่ง Washed / Wet  เป็นวิธีการผลิตที่มีโอกาสผ่าน Specialty coffee น้อยที่สุดอยู่ที่ 85.7% แต่เมล็ดกาแฟจาก Ethiopia สามารถที่จะทำคะแนนได้ถึงอันดับที่ 1 จากข้อมูลทั้งหมด


![image](https://github.com/Mixsung27/Arabica-analysis/assets/135399656/b283854c-5d6d-4b1d-aa23-348c23bfab59)

สรุปแล้วกระบวนการผลิตกาแฟที่แตกต่างกันนั้นมีผลต่อคะแนนรสสัมผัสของกาแฟค่อนข้างมาก แต่ไม่ใช่ทั้งหมด ส่วนที่มีผลต่อรสชาติของกาแฟไม่แพ้กัน คือ คุณภาพของเมล็ดกาแฟตั้งแต่แหล่งกำเนิด
