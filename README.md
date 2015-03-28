# Soril1
#bodlogo3

#include "D:\Hicheel\PIC code\soril1_3.h"
#define led PIN_D0
#bit tmr1on=0xFCD.0

char n;
float data[10],sum=0;
int i=0,j;

#int_TIMER1
TIMER1_isr() 
{
   set_timer1(55535);
   n=read_adc();
   data[i]=n*0.01965;
   i++;
   if(i==11) i=0;
}



void main()
{

   setup_adc_ports(AN0);
   setup_adc(ADC_CLOCK_INTERNAL);
   setup_psp(PSP_DISABLED);
   setup_spi(FALSE);
   setup_timer_0(RTCC_INTERNAL|RTCC_DIV_1);
   setup_timer_1(T1_INTERNAL|T1_DIV_BY_2);
   set_timer1(55535);
   setup_timer_2(T2_DISABLED,0,1);
   setup_comparator(NC_NC_NC_NC);
   setup_vref(FALSE);
   enable_interrupts(INT_TIMER1);
   enable_interrupts(GLOBAL);

   // TODO: USER CODE!!
   set_tris_d(0x00);
   set_adc_channel(0);
   tmr1on=1;
   
   while(1)
   {
      output_toggle(led);
      delay_ms(200);
      sum=0;
      if(i==10)
      {
         for(j=0;j<=10;j++)
         {
            sum=sum+data[j];
         }
         i=0;
         printf("%f \r\n",sum/10);        
      }
   }
}
