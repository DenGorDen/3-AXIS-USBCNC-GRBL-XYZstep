# GRBL 1.1 to 3-AXIS step driver 28byj-48
За основу взято проект https://github.com/robomechs/6-AXIS-USBCNC-GRBL у якому було модифіковано файл cpu_map.h для керування кроковими двигунами в режимі цілого кроку.
Підключення двигунів 28byj-48 до плати stm32f103 :

  //	Port A  
  //	0  Y1_STEP_BIT  
  //	1  Y2_STEP_BIT  
  //	2  Y3_STEP_BIT  
  //	3  Y4_STEP_BIT  
  //	4  Z1_STEP_BIT  
  //	5  Z2_STEP_BIT  
  //	6  Z3_STEP_BIT  
  //	7  Z4_STEP_BIT  
  //	8  SPINDLE_PWM_BIT  
  //	9  PROBE  
  //	10 reserved  
  //	11 usb  
  //	12 usb  
  //	13 swd 
  //	14 swd  
  //	15 STEPPERS_DISABLE_BIT  
  
  //	Port B  
  //	0  SPINDLE_DIRECTION_BIT  
  //	1  SPINDLE_ENABLE_BIT  
  //	2  unconnected  
  //	3  COOLANT_MIST_BIT  
  //	4  COOLANT_FLOOD_BIT  
  //	5  CONTROL_RESET_BIT  
  //	6  CONTROL_FEED_HOLD_BIT  
  //	7  CONTROL_CYCLE_START_BIT  
  //	8  CONTROL_SAFETY_DOOR_BIT  
  //	9  X1_STEP_BIT  
  //	10 X2_STEP_BIT  
  //	11 X3_STEP_BIT  
  //	12 X4_STEP_BIT  
  //	13 X_LIMIT_BIT  
  //	14 Y_LIMIT_BIT  
  //	15 Z_LIMIT_BIT  
  

  Внесено змінну #define XYZ_AXIS_step до config.h для роботи проекту.
   Продубльовані налаштування для роботи проекту у файлі defaults.h у режимі XYZ_AXIS_step.
   Модифіковано також файли stepper.c, додано код у режимі XYZ_AXIS_step.
   Частота кроку становить 137 гц, що дозволяє підключити кроковий двигун 28byj-48 (100 гц).
   Реалізовано два режими роботи двигунів для кожної осі: повний крок та півкрок.
   Встановлення режиму через $1 (Step idle delay, milliseconds) аналогічно параметру $2 (Step pulse invert, mask).  
0=(X+ Y+ Z+)    
1=(X- Y+ Z+)    
2=(X+ Y- Z+)    
3=(X- Y- Z+)    
4=(X+ Y+ Z-)    
5=(X- Y+ Z-)    
6=(X+ Y- Z-)    
7=(X- Y- Z-)    
  Якщо закоментувати #define XYZ_AXIS_step і розкоментувати #define ABC_AXIS_EXAMPLE проект повернеться 
   у вихідний стан як https://github.com/robomechs/6-AXIS-USBCNC-GRBL
   
   Готова прошивка лежить у папці Debug, проект скомпільований в Atollic TrueSTUDIO 
