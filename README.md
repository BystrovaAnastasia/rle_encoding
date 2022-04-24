# RLE-кодирование
RLE-кодирование (Сжатие и и развертка черно-белого двумерного изображения)

```
package com.company;

import java.util.ArrayList;
import java.util.Collections;

public class Main
{
    public static void main(String[] args) {

        String[] Z = {"11111111", "11111111", "11111111", "11111111", "11111111", "11110000", "00001111", "11000011", "10101010", "10101010",
                "10101010", "10101010", "10101010", "10101010"};

        System.out.println("PACKING:");
        System.out.println();

        int l = Z.length;
        int k = 0;

        ArrayList<String> list = new ArrayList<String>();
        ArrayList<Integer> lcount = new ArrayList<Integer>();
        ArrayList<String> lbi = new ArrayList<String>();

        for (int i = 0; i < Z.length; i++){
            list.add(Z[i]);
        }

        for (int i=0; i<list.size(); i++){
            System.out.print(list.get(i) + " ");
        }

        System.out.println();
        System.out.println();

        int count = 0;
        String lchar = list.get(0);
        for (int i=0; i<list.size(); i++){
            if (list.get(i)==lchar){
                count++;
            }
            else{
                lchar = list.get(i);
                lcount.add(count);
                lbi.add(list.get(i-1));
                count = 1;
            }
        }
        lbi.add(list.get(list.size()-1));
        lcount.add(count);
        for (int i = 0; i<lbi.size(); i++)
            System.out.println("[" + lbi.get(i) + "] - " + lcount.get(i));

        System.out.println();
        ArrayList<String> ltemp = new ArrayList<String>();

        int templ=0;
        for (int i=0; i<lcount.size(); i++){
            templ = lcount.get(i);
            if (templ>1){
                int b;
                String temp = "";
                while(templ!=0){
                    b = templ%2;
                    temp = b + temp;
                    templ = templ/2;
                }
                while(temp.length()!=7){
                    temp = "0"+temp;
                }
                temp = "1"+temp;
                ltemp.add(temp);
            }
            else{
                templ = lcount.get(i);
                int b;
                String temp = "";
                while(templ!=0){
                    b = templ%2;
                    temp = b + temp;
                    templ = templ/2;
                }
                while(temp.length()!=8){
                    temp = "0"+temp;
                }
                ltemp.add(temp);
            }
        }

        for (int i=0; i<ltemp.size(); i++){
            System.out.println(ltemp.get(i));
        }

        ArrayList<String> lfin = new ArrayList<String>();
        ArrayList<String> lt = new ArrayList<String>();

        count=0;
        int n=0;
        while(n<lcount.size()){
            if (lcount.get(n)==1){
                while(lcount.get(n)==1){
                    lt.add(lbi.get(n));
                    count++;
                    n++;
                }
                templ = count;
                int b;
                String temp = "";
                while(templ!=0){
                    b = templ%2;
                    temp = b + temp;
                    templ = templ/2;
                }
                while(temp.length()!=8){
                    temp = "0"+temp;
                }
                lfin.add(temp);
                for(int j=0; j<lt.size(); j++){
                    lfin.add(lt.get(j));
                }
                count=0;
            }
            else{
                lfin.add(ltemp.get(n));
                lfin.add(lbi.get(n));
                n++;
            }
        }

        System.out.println();

        for (int i=0; i<lfin.size(); i++){
            System.out.print(lfin.get(i) + " ");
        }

        System.out.println();
        System.out.println("Compression ratio: "+(double)lfin.size()/list.size());

///////////////////////////////////////////////////////////////////////////

        System.out.println();
        System.out.println("UNPACKING:");
        System.out.println();
        for (int i=0; i<lfin.size(); i++){
            System.out.print(lfin.get(i) + " ");
        }

        ArrayList<String> lst = new ArrayList<String>();

        int m = 0;
        while (m < lfin.size()){
            count = Integer.parseInt(lfin.get(m).substring(1), 2);
            if (lfin.get(m).substring(0,1).equals("1")){
                for(int i=0; i<count; i++){
                    lst.add(lfin.get(m+1));
                }
                m++;
            }
            else{
                if (lfin.get(m).substring(0,1).equals("0")){
                    for (int i=1; i<=count; i++){
                        m++;
                        lst.add(lfin.get(m));
                    }
                }
            }
            m++;
        }

        System.out.println();
        System.out.println();

        for (int i=0; i<lst.size(); i++){
            System.out.print(lst.get(i) + " ");
        }
    }
}
```
