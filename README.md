***** AIM *****
This Perl code implements well-known logic locking techniques at RTL including CAC 2.0, which is resilient to existing SAT-based, removal, and structural analysis attacks. 

***** USAGE *****
The usage of the Perl code can be given as follows which can be obtained after running the "perl hiid.pl -h" command:

Usage:       perl hiid.pl -b=<FileName> -v=<FileName> -p=<FileName> -t=0-3 -nok=<int> -pip=<int> -dbl=<int> -mli -rll=<int> -rtl -orl -lec -seed=<int> -rm -verb -h                   
b:           Original circuit in bench                                                                                                                                                
v:           Original circuit in Verilog                                                                                                                                              
p:           File including paths to solvers tools and design libraries by default it is paths.pl                                                                                     
t:           Logic locking technique by default it is CAC                                                                                                                             
               0: ANTISAT                                                                                                                                                             
               1: SARLock                                                                                                                                                             
               2: TTLock                                                                                                                                                              
               3: CAC                                                                                                                                                                 
nok:         Number of key bits for a given logic locking technique by default it is 16                                                                                               
pip:         Number of input patterns to be protected when t is 1/3 by default it is 1                                                                                                
dbl:         Locks the locked circuit using CAC with given maximum number of key bits when t is 2/3 by default it does not                                                            
mli:         Obfuscates the protected primary inputs using decoy primary inputs when t is 3 by default it does not                                                                    
rll:         Initially locks the original circuit using RLL with given number of key bits by default it does not                                                                      
rtl:         Assumes that the Verilog file is defined at behavioral level by default it does not                                                                                      
orl:         Regenerates a locked circuit with different protected input pattern(s) up to 10 times until the original circuit does not reside in the locked one by default it does not
lec:         Runs LEC to check if the original design is equivalent to the locked one under the secret key by default it does not                                                     
seed:        Seed for the random number generator by default it is 1                                                                                                                  
rm:          Removes unnecessary files by default it does not                                                                                                                         
verb:        Prints comments during execution by default it does not                                                                                                                  
h:           Prints this screen                                                                                                                                                       
Description: This code implements various logic locking techniques including CAC 2.0                                                                                                  
Notes:       ANTI-SAT and TTLock works when pip is 1                                                                                                                                  
             Locking a locked circuit using CAC works when t is 2/3                                                                                                                   
             Obfuscation of protected primary input works when t is 3                                                                                                                 
             CAC 2.0 works when t is 3 mli is selected and dbl value is set. Note that the sum of nok and dbl values determines the total number of key inputs considering mli        
             When the original design is described at behavioral level using bit arrays for primary inputs and outputs as in the arith_unit.v file the rtl option should be used      
Examples:    perl hiid.pl -v=../examples/c2670.v -t=0 -nok=64 -rm -lec -v                        //ANTI-SAT with 64 key inputs                                                        
             perl hiid.pl -v=../examples/c2670.v -t=1 -nok=32 -rm -lec -v                        //SARLock with 32 key inputs                                                         
             perl hiid.pl -v=../examples/c2670.v -t=2 -nok=32 -rm -lec -v                        //TTLock with 32 key inputs                                                          
             perl hiid.pl -v=../examples/c2670.v -t=3 -nok=32 -rm -lec -v                        //CAC with 32 key inputs                                                             
             perl hiid.pl -v=../examples/c2670.v -t=0 -nok=64 -rll=32 -rm -lec -v                //RLL+ANTI-SAT with 32+64 key inputs                                                 
             perl hiid.pl -v=../examples/c2670.v -t=1 -nok=32 -rll=32 -rm -lec -v                //RLL+SARLock with 32+32 key inputs                                                  
             perl hiid.pl -v=../examples/c2670.v -t=2 -nok=32 -rll=32 -rm -lec -v                //RLL+TTLock with 32+32 key inputs                                                   
             perl hiid.pl -v=../examples/c2670.v -t=3 -nok=32 -rll=32 -rm -lec -v                //RLL+CAC with 32+32 key inputs                                                      
             perl hiid.pl -v=../examples/c2670.v -t=3 -nok=64 -dbl=32 -mli -rm -lec -v           //CAC 2.0 with 64+32 key inputs                                                      
             perl hiid.pl -v=../examples/c2670.v -t=3 -nok=64 -dbl=32 -mli -orl -rm -lec -v      //CAC 2.0 with 64+32 key inputs using orl option                                     
             perl hiid.pl -v=../examples/arith_unit.v -t=3 -nok=16 -dbl=8 -mli -rtl -rm -lec -v  //CAC 2.0 with 16+8 key inputs using rtl option                                      

***** IO FILES *****
HIID takes the original circuit in bench or Verilog as an input and returns the locked circuit in bench and Verilog.

***** DEPENDENCIES *****
HIID requires Cadence Genus for logic synthesis, Cadence Conformal for formal verification, ABC for bench and Verilog file conversion, and SAT algorithm for equivalance checking.
ABC can be obtained from https://github.com/berkeley-abc/abc and the SAT solver cryptominisat can be obtained from https://www.msoos.org/cryptominisat5/
Since a design library is required for logic synthesis, the open source Nangate 45 nm design library is provided.
The locations of tools, solvers, and design libraries should be given in a file. Please check the "paths.pl" file as an example.
HIID was tested under Linux running Perl v5.26.1 and Cadence 2019 EDA version with Nangate 45 nm design library.

***** CONTACT *****
Please contact Levent Aksoy (leventaksoy@taltech.ee) if you have any trouble running the code and suggestions and/or comments.

