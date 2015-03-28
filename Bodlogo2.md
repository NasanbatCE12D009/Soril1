#include "D:\Hicheel\PIC code\Soril1_2.h"
#define led PIN_D0

char n,k;
float volt1,volt2;

void main()
{

   setup_adc_ports(AN0_AN1_VSS_VREF);
   setup_adc(ADC_CLOCK_INTERNAL);
   setup_psp(PSP_DISABLED);
   setup_spi(FALSE);
   setup_timer_0(RTCC_INTERNAL|RTCC_DIV_1);
   setup_timer_1(T1_DISABLED);
   setup_timer_2(T2_DISABLED,0,1);
   setup_comparator(NC_NC_NC_NC);
   setup_vref(FALSE);

   // TODO: USER CODE!!
   
   
   while(1)
   {
      // adc gees utgaa unshih
      set_adc_channel(0);
      n=read_adc();
      set_adc_channel(1);
      k=read_adc(); 
      
      // adc giin toon utgiig volt ruu horwuulne
      volt1=25*n+15.8;
      volt2=100*k+20.5;
      
      // nohtsoloo shalgana
      if((volt1>25 && volt1<50) && (volt2>100 && volt2<200))
      {
         printf("Hewiin \r\n");
      }
      else
      {
         output_toggle(led);
         printf("warning \r\n");
         delay_ms(300);
      }
   }
}
