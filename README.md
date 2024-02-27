# 3-AXIS-USBCNC-GRBL-XYZstep
GRBL 1.1 for 3-AXIS + step driver 28byj-48

За основу взято проект https://github.com/robomechs/6-AXIS-USBCNC-GRBL у якому було модифіковано файл cpu_map.h для керування кроковими двигунами в режимі цілого кроку.
Підключення двигунів 28byj-48 до плати stm32f103 :

  //	Port A                    						Port B
  //	0  Y1_STEP_BIT					        		SPINDLE_DIRECTION_BIT
  //	1  Y2_STEP_BIT					        		SPINDLE_ENABLE_BIT
  //	2  Y3_STEP_BIT									    unconnected
  //	3  Y4_STEP_BIT								      COOLANT_MIST_BIT
  //	4  Z1_STEP_BIT							   	    COOLANT_FLOOD_BIT
  //	5  Z2_STEP_BIT								      CONTROL_RESET_BIT
  //	6  Z3_STEP_BIT								      CONTROL_FEED_HOLD_BIT
  //	7  Z4_STEP_BIT								      CONTROL_CYCLE_START_BIT
  //	8  SPINDLE_PWM_BIT							    CONTROL_SAFETY_DOOR_BIT
  //	9  PROBE	                	        X1_STEP_BIT
  //	10 reserved for UART1 	            X2_STEP_BIT
  //	11 usb											        X3_STEP_BIT
  //	12 usb										        	X4_STEP_BIT
  //	13 swd, 	                      		X_LIMIT_BIT
  //	14 swd, 	                        	Y_LIMIT_BIT
  //	15 STEPPERS_DISABLE_BIT							Z_LIMIT_BIT

   Внесено змінну #define XYZ_AXIS_step до config.h для роботи проекту.
   Продубльовані налаштування для роботи проекту у файлі defaults.h у режимі XYZ_AXIS_step.
   Модифіковано також файли stepper.c, додано код у режимі XYZ_AXIS_step.
   Частота кроку становить 137 гц, що дозволяє підключити кроковий двигун 28byj-48 (100 гц).
   Можна трохи змінити початковий шаблон кроку current_ _step = 0001, або 0011, для імітації півкроку.
   режим півкроку не реалізовано.
   якщо закоментувати #define XYZ_AXIS_step і розкоментувати #define ABC_AXIS_EXAMPLE проект повернеться 
   у вихідний стан як https://github.com/robomechs/6-AXIS-USBCNC-GRBL
   готова прошивка лежить у папці Debug, проект скомпільований в Atollic TrueSTUDIO 
