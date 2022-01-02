# youssef
self driving car by VHDL
########################################### code
########################################################################################### 
library ieee;
use ieee.std_logic_1164.all;
 
entity selfdrivingcar is
    Port ( clk,rst,start,s1,cs1,cs2,s2,s3,Ai1,tr,s4,v40,hl,v70,hr,g,tu,right,dest : in STD_LOGIC;
 
 
           sc,sen,ca,Ai,stop,rl,ll,v,cl,llight,rlight,gps,sd,e,traffic,cd,obst: out STD_LOGIC);
end selfdrivingcar;
 
architecture Behavioral of selfdrivingcar is
type state is(T0,T1,T2,T3,T4,T5,T6,T7,T8,T9,T10,T11,T12,T13,T14,T15,T16,T17,T18,T19,T20,T21,T22,T23);
signal pr,nxt:state;
begin
    seq:process(clk)
    begin
    if rising_edge(clk) then 
      if (rst='1') 
                then 
                    pr<=T0;
                else
                    pr<=nxt;
              end if;
     end if;
     end process seq;
     comb:process(pr,start,s1,cs1,cs2,s2,s3,Ai1,tr,s4,v40,HL,v70,Hr,g,tu,right,dest)
     begin 
     case pr is
     when T0=>
     e<='0'; sc<='0';
     sen<='0'; ca<='0';
     Ai<='0'; stop<='0';
     rl<='0'; ll<='0'; cl<='0';
     llight<='0'; rlight<='0';
     gps<='0'; sd<='0';
     cd<='0';traffic<='0';
     obst<='0'; v<='0';
        if(start='1')then 
        nxt<=T1;
        else 
         nxt<=T0;
        end if;
     when T1=>
     e<='1';
     cd<='1';
        if (s1='1')then 
        nxt<=T2;
        else
        nxt<=T1;
        end if;
     when T2=>
     sc<='1';
        if(cs1='1') then nxt<=T3;
        else
         nxt<=T2;
        end if;
     when T3=>
     gps<='1';
        if(cs2='1') then nxt<=T4;
        else nxt<=T3;
        end if;
      when T4=>
      sen<='1';
        if(s2='1') then nxt<=T5;
        else nxt<=T4;
        end if;
     when T5=>
     ca<='1';
        if(s3='1') then nxt<=T6;
        else nxt<=T5;
        end if;
     when T6=>
     Ai<='1';
     v<='1';
        if(Ai1='1') then nxt<=T7;
        else nxt<=T6;
        end if;
     when T7=>
     traffic<='1';
        if(tr='1')  then 
            if(g='1')  then nxt<=T8;
            else nxt<=T9;
            end if;
        else nxt<=T8;
        end if;
     when T8=>
     obst<='1';
        if(s4='1') then nxt<=T9;
        else nxt<=T10;
        end if;
     when T9=>
     sd<='1';
     stop<='1';
     v<='0';
     obst<='0';
     nxt<=T7;
     when T10=>
     sd<='0';
     stop<='0';
     v<='1';
        if(v40='1') then nxt<=T11;
        else nxt<=T13;
        end if;
     when T11=>
     rl<='1';
     nxt<=T12;
     when T12=>
     obst<='1';
     rl<='0';
      if(s4='1') then nxt<=T7;
      else nxt<=T16;
      end if;
    when T13=>
    obst<='0';
    llight<='1';
        if(hl='1')
            then   
            if(v70='1') then nxt<=T14;
            else nxt<=T15;
            end if;       
        else  
        nxt<=T13;
        end if;
        when T14=>
        llight<='0';
        ll<='1';
        nxt<=T12;
        when T15=>
        ll<='0';
        cl<='1';
        nxt<=T15;
        when T16=>
        cl<='0';
            if( tu='0')  then nxt<=T16;
            else nxt<=T17;
            end if;
         when T17=>
         sd<= '1';
            if ( right='1') then 
            nxt <= T20 ;
            else nxt<=T18 ;
            end if ;
         when T18 => 
         sd<='0' ;
         llight<= '1' ;
            if (hl='1') then 
            nxt <= T19 ;
            else nxt<=T18 ;
            end if ;
         when T19=>  
         llight <= '0' ;
         ll<='1' ;
            nxt <= T22 ;
         when T20 => 
         ll<='0' ;
         

             rlight<='1' ;
            if (hr='1') then nxt<=T21 ;
            else nxt<=T20 ;
            end if; 
         when T21=> 
         rlight <='0' ;
         rl<='1'; 
            nxt<=T22; 
         when T22=> 
         rl<='0' ;
            if (s4='1')then nxt<=T7 ;
            else 
                if (dest='1') then nxt<=T23 ;
                else nxt<=T16 ;
                end if ;
             end if;
          when T23=>
          nxt<=T0 ;
 
 
     end case;
     end process comb; 

end Behavioral;
