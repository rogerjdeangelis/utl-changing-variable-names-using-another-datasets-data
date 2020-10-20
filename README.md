# utl-changing-variable-names-using-another-datasets-data
Changing variable names using another dataset’s data
    Changing variable names using another dataset’s data                                                                   
                                                                                                                           
    GitHub                                                                                                                 
    https://tinyurl.com/y2hfczeq                                                                                           
    https://github.com/rogerjdeangelis/utl-changing-variable-names-using-another-datasets-data                             
                                                                                                                           
       Two Solutions                                                                                                       
             a. Ted Clay tclay@ashlandhome.net macro array abd do_over                                                     
             b. Bart's more flexible macro array and do_over                                                               
                Simpler                                                                                                    
                                                                                                                           
    I need to change a large number of variable names of a dataset.                                                        
    The targeted names are included in another dataset as data.                                                            
    For example, there are two datasets, A and B.                                                                          
    The variable names of A are a1 a2 a3. And B has two variables,                                                         
    of which names are b1 and b2. b2 has data: c1, c2, and c3.                                                             
    Then I want to replace a1-3 by c1-3. Could you please help?                                                            
                                                                                                                           
    macros                                                                                                                 
    https://tinyurl.com/y9nfugth                                                                                           
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories                             
                                                                                                                           
    SAS Forum                                                                                                              
    https://tinyurl.com/yxermbyt                                                                                           
    https://communities.sas.com/t5/SAS-Programming/Changing-variable-names-using-another-dataset-s-data/m-p/692003         
                                                                                                                           
    /*                   _                                                                                                 
    (_)_ __  _ __  _   _| |_                                                                                               
    | | `_ \| `_ \| | | | __|                                                                                              
    | | | | | |_) | |_| | |_                                                                                               
    |_|_| |_| .__/ \__,_|\__|                                                                                              
            |_|                                                                                                            
    */                                                                                                                     
    data work.have;                                                                                                        
      x = 1; y = 'Y'; output;                                                                                              
    run;                                                                                                                   
                                                                                                                           
    WORK.HAVE total obs=1                                                                                                  
                                                                                                                           
    Obs    X    Y                                                                                                          
                                                                                                                           
     1     1    Y                                                                                                          
                                                                                                                           
    data renames;                                                                                                          
      oldname = "X"; NewName = "X_NEW"; OUTPUT;                                                                            
      oldname = "Y"; NewName = "Y_NEW"; OUTPUT;                                                                            
    run;                                                                                                                   
                                                                                                                           
    WORK.RENAMES total obs=2                                                                                               
                                                                                                                           
    Obs    OLDNAME    NEWNAME                                                                                              
                                                                                                                           
     1        X        X_NEW                                                                                               
     2        Y        Y_NEW                                                                                               
                                                                                                                           
    /*           _               _                                                                                         
      ___  _   _| |_ _ __  _   _| |_                                                                                       
     / _ \| | | | __| `_ \| | | | __|                                                                                      
    | (_) | |_| | |_| |_) | |_| | |_                                                                                       
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                      
                    |_|                                                                                                    
    */                                                                                                                     
                                                                                                                           
    HAVE total obs=1                                                                                                       
                                                                                                                           
    Obs    X_NEW    Y_NEW                                                                                                  
                                                                                                                           
     1       1        Y                                                                                                    
                                                                                                                           
    /*         _       _   _                                                                                               
     ___  ___ | |_   _| |_(_) ___  _ __  ___                                                                               
    / __|/ _ \| | | | | __| |/ _ \| `_ \/ __|                                                                              
    \__ \ (_) | | |_| | |_| | (_) | | | \__ \                                                                              
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/                                                                              
                                                                                                                           
    /*         _____        _    ____ _                                                                                    
      __ _    |_   _|__  __| |  / ___| | __ _ _   _                                                                        
     / _` |     | |/ _ \/ _` | | |   | |/ _` | | | |                                                                       
    | (_| |_    | |  __/ (_| | | |___| | (_| | |_| |                                                                       
     \__,_(_)   |_|\___|\__,_|  \____|_|\__,_|\__, |                                                                       
                                              |___/                                                                        
    */                                                                                                                     
    */                                                                                                                     
                                                                                                                           
    %array(old,data=renames,var=oldname);                                                                                  
    %array(new,data=renames,var=newname);                                                                                  
                                                                                                                           
    proc datasets lib=work;                                                                                                
                                                                                                                           
      modify have;                                                                                                         
        rename                                                                                                             
      %do_over(old new, phrase=%str(                                                                                       
           ?old =?new                                                                                                      
           ));                                                                                                             
                                                                                                                           
    ;run;quit;                                                                                                             
                                                                                                                           
    /*        _                _                                                                                           
    | |__    | |__   __ _ _ __| |_                                                                                         
    | `_ \   | `_ \ / _` | `__| __|                                                                                        
    | |_) |  | |_) | (_| | |  | |_                                                                                         
    |_.__(_) |_.__/ \__,_|_|   \__|                                                                                        
                                                                                                                           
    */                                                                                                                     
                                                                                                                           
                                                                                                                           
    Bartosz Jablonski                                                                                                      
    Oct 16, 2020, 3:40 PM (4 days ago)                                                                                     
    to me, SAS-L@LISTSERV.UGA.EDU                                                                                          
                                                                                                                           
    Roger,                                                                                                                 
                                                                                                                           
    Let me "shamelessly advertise my own merchandise" :-) :-)                                                              
    Use the macroArray package.                                                                                            
                                                                                                                           
    All the best                                                                                                           
    Bart                                                                                                                   
                                                                                                                           
    data work.have;                                                                                                        
      x = 1; y = 'Y'; output;                                                                                              
    run;                                                                                                                   
                                                                                                                           
    data renames;                                                                                                          
      oldname = "X"; NewName = "X_NEW"; OUTPUT;                                                                            
      oldname = "Y"; NewName = "Y_NEW"; OUTPUT;                                                                            
    run;                                                                                                                   
                                                                                                                           
    filename packages "%sysfunc(pathname(work))"; /* setup temporary directory for packages in the WORK */                 
    filename SPFinit url "https://raw.githubusercontent.com/yabwon/SAS_PACKAGES/master/SPF/SPFinit.sas";                   
    %include SPFinit; /* enable the framework */                                                                           
                                                                                                                           
    %installPackage(macroArray) /* install the package */                                                                  
    %loadPackage(macroArray)    /* load the package content into the SAS session */                                        
                                                                                                                           
    /* %helpPackage(macroArray,'%array()') */                                                                              
    /* %helpPackage(macroArray,'%do_over()') */                                                                            
                                                                                                                           
    %array(ds=renames, vars=oldname#old newname#new, macarray=Y);                                                          
                                                                                                                           
    proc datasets lib=work;                                                                                                
                                                                                                                           
      modify have;                                                                                                         
        rename                                                                                                             
      %do_over(old, phrase=%nrstr(                                                                                         
           %old(&_I_) = %new(&_I_)                                                                                         
           ));                                                                                                             
                                                                                                                           
    ;                                                                                                                      
    run;                                                                                                                   
    quit;                                                                                                                  
                                                                                                                           
    %unloadPackage(macroArray)                                                                                             
                                                                                                                           
