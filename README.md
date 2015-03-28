# Soril1
#bodlogo1
#include "D:\Hicheel\PIC code\ADC.h"

 char n;
 float volt;
 
void main()
{

   setup_adc_ports(AN0);
   setup_adc(ADC_CLOCK_INTERNAL);
   setup_psp(PSP_DISABLED);
   setup_spi(FALSE);
   setup_timer_0(RTCC_INTERNAL|RTCC_DIV_1);
   setup_timer_1(T1_DISABLED);
   setup_timer_2(T2_DISABLED,0,1);
   setup_comparator(NC_NC_NC_NC);
   setup_vref(FALSE);

   // TODO: USER CODE!!
   set_adc_channel(0);  //adc giin utgiig 0 dugaar suwgaar unshij awah
   
   while(1)
   {
       n=read_adc();   // n huwisagchid adc giin toon utgiig onooh 
       volt=n*0.01965; // 5v/255=0.019 buyu adc giin hchdeliin utgiig oloh
       if(volt>=1.5 && volt <=3.0) printf("Normal \r\n"); // herew 15 < volt < 3  baiwal normal hewleh
       else if( volt>3.0) printf("Upper level \r\n"); // 3 < volt baiwal Upper level hewleh
       else printf("Lower limit \r\n");  // busad ued Lower limit hewleh
       delay_ms(300);
   }
}
