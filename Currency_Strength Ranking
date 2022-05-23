#property strict
#property copyright ""
#property link ""

#property indicator_separate_window
//#property indicator_maximum 1
//#property indicator_minimum -1

#property indicator_level1 0

#property indicator_buffers 8
#property indicator_color1 clrCrimson
#property indicator_color2 clrAqua
#property indicator_color3 clrPurple
#property indicator_color4 clrGreen
#property indicator_color5 clrBlue
#property indicator_color6 clrOrange
#property indicator_color7 clrRed
#property indicator_color8 clrWhite



double AUD[], CAD[], CHF[], EUR[], GBP[], JPY[], NZD[], USD[];

string B = StringSubstr(Symbol(),0,3);
string Q = StringSubstr(Symbol(),3,3);

string AllPairs[28] = {
   "EURAUD", // 0
   "EURCAD", // 1
   "EURCHF", // 2
   "EURGBP", // 3
   "EURJPY", // 4
   "EURNZD", // 5
   "EURUSD", // 6
   "GBPAUD", // 7
   "GBPCAD", // 8
   "GBPCHF", // 9
   "GBPJPY", // 10
   "GBPNZD", // 11
   "GBPUSD", // 12
   "AUDCAD", // 13
   "AUDCHF", // 14
   "AUDJPY", // 15
   "AUDNZD", // 16
   "AUDUSD", // 17
   "NZDCAD", // 18
   "NZDCHF", // 19
   "NZDJPY", // 20
   "NZDUSD", // 21
   "USDCAD", // 22
   "USDCHF", // 23
   "USDJPY", // 24
   "CADCHF", // 25
   "CADJPY", // 26
   "CHFJPY" // 27 total = 28
};


//+------------------------------------------------------------------+
//| Custom indicator initialization function |
//+------------------------------------------------------------------+
int init()
  {
  
  int e = 1, g = 1, a = 1, n = 1;
  int u = 1, c = 1, f = 1, j = 1;
 
  int E = 2, G = 2, A = 2, N = 2;
  int U = 2, C = 2, F = 2, J = 2;
 
if((B=="EUR") || (Q == "EUR")) {E = 0; e = 3;}
if((B=="GBP") || (Q == "GBP")) {G = 0; g = 3;}
if((B=="AUD") || (Q == "AUD")) {A = 0; a = 3;}
if((B=="NZD") || (Q == "NZD")) {N = 0; n = 3;}
if((B=="USD") || (Q == "USD")) {U = 0; u = 3;}
if((B=="CAD") || (Q == "CAD")) {C = 0; c = 3;}
if((B=="CHF") || (Q == "CHF")) {F = 0; f = 3;}
if((B=="JPY") || (Q == "JPY")) {J = 0; j = 3;}
 
//---- indicators setting
   SetIndexStyle(0,DRAW_LINE,E,e);
   SetIndexStyle(1,DRAW_LINE,G,g);
   SetIndexStyle(2,DRAW_LINE,A,a);
   SetIndexStyle(3,DRAW_LINE,N,n);
   SetIndexStyle(4,DRAW_LINE,U,u);
   SetIndexStyle(5,DRAW_LINE,C,c);
   SetIndexStyle(6,DRAW_LINE,F,f);
   SetIndexStyle(7,DRAW_LINE,J,j);


   IndicatorDigits(0);
  IndicatorShortName("Bloup2");

   SetIndexBuffer(0,EUR);
   SetIndexLabel(0,"EUR ");

   SetIndexBuffer(1,GBP);
   SetIndexLabel(1,"GBP ");

   SetIndexBuffer(2,AUD);
   SetIndexLabel(2,"AUD ");

   SetIndexBuffer(3,NZD);
   SetIndexLabel(3,"NZD ");

   SetIndexBuffer(4,USD);
   SetIndexLabel(4,"USD ");

   SetIndexBuffer(5,CAD);
   SetIndexLabel(5,"CAD ");

   SetIndexBuffer(6,CHF);
   SetIndexLabel(6,"CHF ");

   SetIndexBuffer(7,JPY);
   SetIndexLabel(7,"JPY ");

   return(0);
  }

//+------------------------------------------------------------------+
//| Custom indicator iteration function |
//+------------------------------------------------------------------+
int OnCalculate(const int rates_total,
                const int prev_calculated,
                const datetime &time[],
                const double &open[],
                const double &high[],
                const double &low[],
                const double &close[],
                const long &tick_volume[],
                const long &volume[],
                const int &spread[]){


 
  int counted_bars=IndicatorCounted();
      if(counted_bars<0) return(-1);
      if(counted_bars>0) counted_bars--;
           int limit=MathMin(Bars-counted_bars,Bars-1);
  
//---- indicator calculation

  for(int i=limit; i>=0; i--)
     {


  
EUR[i]=GetLastC("EUR",PERIOD_CURRENT,i);

GBP[i]=GetLastC("GBP",PERIOD_CURRENT,i);

AUD[i]=GetLastC("AUD",PERIOD_CURRENT,i);

NZD[i]=GetLastC("NZD",PERIOD_CURRENT,i);

USD[i]=GetLastC("USD",PERIOD_CURRENT,i);

CAD[i]=GetLastC("CAD",PERIOD_CURRENT,i);

CHF[i]=GetLastC("CHF",PERIOD_CURRENT,i);

JPY[i]=GetLastC("JPY",PERIOD_CURRENT,i);
  
 //---
   
     }


//----
   return(0);
  }
//+------------------------------------------------------------------+
double GetLastC(string symb, int tf, int shift)
//+------------------------------------------------------------------+
{
   double res = 0;
   double pres = 0;
   double nres = 0;

   for(int x = 0; x < ArraySize(AllPairs); x++) {

      int pos = StringFind(AllPairs[x], symb, 0);
      if(pos == 0 || pos == 3) {

         double b      = iOpen(AllPairs[x],tf,shift);
         double r      = iClose(AllPairs[x],tf,shift);

         if((pos == 0 && r > b)
            || (pos == 3 && r < b)) pres++;

         if((pos == 0 && r < b)
            || (pos == 3 && r > b)) nres++;

      }
   }

   if(pres > nres) res=pres;
   if(pres < nres) res=-nres;

   return(res);
}


 //+------------------------------------------------------------------+
double DivZero(double n, double d)
//+------------------------------------------------------------------+
// Divides N by D, and returns 0 if the denominator (D) = 0
// Usage:   double x = DivZero(y,z)  sets x = y/z
{
  if (d == 0) return(0);  else return(n/d);
}  
