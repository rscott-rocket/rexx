A very small repo of REXX external functions that can add to the IBM-supplied functions

These programs typically run unauthorized, problem state and in the key of the caller.

To build the load module run some JCL similar to the following replacing "userid" and 
"program" accordingly.

Note that the names or SASMMAC2, MACLIB and MODGEN might be different at your site

//ASM  EXEC PGM=ASMA90,PARM='RENT',REGION=16000K                     
//SYSPRINT DD  SYSOUT=*                                            
//SYSIN    DD  DISP=SHR,DSN=userid.ASM(program)                     
//SYSLIB   DD  DISP=SHR,DSN=ASM.SASMMAC2                           
//         DD  DISP=SHR,DSN=SYS1.MACLIB                            
//         DD  DISP=SHR,DSN=SYS1.MODGEN                            
//SYSUT1   DD  UNIT=SYSDA,SPACE=(CYL,(2,1))                        
//SYSTERM  DD  SYSOUT=*                                            
//SYSADATA DD  DUMMY                                               
//SYSLIN   DD  DISP=SHR,DSN=userid.OBJ(program)                     
//*                                                                
//LINK EXEC PGM=IEWL,PARM='MAP,LET,LIST,XCAL,RENT'
//SYSLMOD  DD  DISP=SHR,DSN=userid.LINKLIB                         
//SYSPRINT DD  SYSOUT=*                                            
//SYSUT1   DD  UNIT=SYSDA,SPACE=(CYL,(2,1))                        
//SYSOBJ   DD  DISP=SHR,DSN=userid.OBJ                             
//SYSLIN   DD  *                                                   
  INCLUDE SYSOBJ(program)                                           
  ENTRY program                                                     
  NAME program(R)                                                   
