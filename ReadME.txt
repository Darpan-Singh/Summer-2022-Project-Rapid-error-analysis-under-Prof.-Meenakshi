DARPAN SINGH (IMT2020133)


*SUMMER PROJECT  : Rapid Code Error Analysis


*Under Guidance of: Prof. Meenkashi  D'Souza ma'am


*Mentored By :   Ph.D. Research Scholar  Ameena K. Ashraf ma'am


Tutorial link :-
https://drive.google.com/file/d/1oioX2_X4MZsTW062qiaPBfNm67kbrIWf/view?usp=sharing


COMPILE AND RUN :-
1.  Open the (TaskAnalyzer.java) file of the (CheckAllRules) package and change the path of your input file for Rule#1 (around line#25), according to  your system. In my case the "flex loader.txt" file in the "InputRules" directory serves as the input to check Rule#1 of WaitSync task and SyncMoveOn-SyncMoveOff task instruction .
2.  Open (ManageWaitUntilTestAndSet.java) file of (Functionality) package and change the path of your input file for Rule#2 (around line#17),  according to  your system. In my case the "rule2.txt" file in the "InputRules" directory serves as the input to check Rule#2.
3.  Open (ManageWaitUntil.java) file of (Functionality) package and change the path of your input file for Rule#3 (around line#15),  according to  your system. In my case the "rule3.txt" file in the "InputFiles" directory serves as the input to check Rule#3.
4.  Open (ManageSetDOISignalDO.java) file of (Functionality) package and change the path of your input file for Rule#4 (around line#16),  according to  your system. In my case the "rule4.txt" file in the "InputFiles" directory serves as the input to check Rule#4.
5.  Open (ManageSetDOWaitDO.java) file of (Functionality) package and change the path of your input file for Rule#5 (around line#16),  according to  your system. In my case the "rule5.txt" file in the "InputFiles" directory serves as the input to check Rule#5.
6.  Open (ManageSharedVarRule.java) file of (Functionality) package and change the path of your input file for Rule#6 (around line#16),  according to  your system. In my case the "rule6.txt" file in the "InputFiles" directory serves as the input to check Rule#6.
7.  Open (ManageIEnableIDisable.java)  file of (Functionality) package and change the path of your input file for Rule#7 (around line#16),  according to  your system. In my case the "rule7.txt" file in the "InputFiles" directory serves as the input to check Rule#7.
8.  Now open the terminal in the src folder (in my case "Darpan/Practice/task analyzer/Rapid-program-parser/src") and type : " javac Functionality/*.java Main/*.java CheckAllRules/*.java " and press Enter.
9.  Then type and run : " java CheckAllRules/TaskAnalyzer "






STRUCTURE OF src FOLDER :-


Package CheckAllRules :
    -TaskAnalyzer.java file
Package Functionality :
    -ManageConditionalStatements.java file
    -ManageIEnableIDisable.java file
    -ManageMove.java file
    -ManageProc.java file
    -ManageSetDOISignalDO.java file
    -ManageSetDOWaitDO.java file
    -ManageSharedVarRule.java file
    -ManageSyncConstructs.java file
    -ManageSyncMoveInstructions.java file
    -ManageVariable.java file
    -ManageWaitInstructions.java file
    -ManageWaitSyncInstructions.java file
    -ManageWaitSyncTaskInstructions.java file
    -ManageWaitUntil.java file
    -ManageWaitUntilTestAndSet.java file
Package InputRules :
    -a.txt file
    -flex loader.txt file   (aka Rule1)
    -rule2.txt file
    -rule3.txt file
    -rule4.txt file
    -rule5.txt file
    -rule6.txt file
    -rule7.txt file
Package Main :
    -Bool_bool.java 
    -Bool_list
    -ConditionalStatements.java file
    -Ident_Task_name.java file
    -MoveInstruction.java file
    -Parser.java file
    -Procedure.java file
    -RobTarget.java file
    -Sync_move_block.java file
    -SyncInstruction.java file
    -Variable.java file
    -WaitInstruction.java file
Package RaceDetector :
    -contains Task analyzer to check datarace and individual java files to check rules






PROJECT OVERVIEW :-


The project basically checks for ERRORS among the different tasks in a multitasking Rapid programs. For that first we implement a Parser for parsing Rapid program tasks. We different functionalities like MangeWaitInstructions,ManageSyncinstructions, etc. We parse through each and every sentences in the program line by line and stored the output. In Rapid we know global variables are declared using PERS in each tasks. So during parsing, they extracted the global variables and store them in "globalTasklist" in the form of LinkedHashmap<String, Bool_lis>, where the bool list comprises of 4 Boolean representing them to be true if they are present in the corresponding Roboy. The next step in our project is analysing the different RULES(1 to 7) defined later, starting with the WaitSyncTask(Rule#1(a)) and SyncMoveOn-SyncMoveOff which is Rule#1(b) (Line 64-65 of CheckAllRules/TaskAnalyzer.java).Then the Rule#2 (Line 66), Rule#3 (Line 67) , Rule#4, ... Rule#7(Line 71) are checked by calling the corresponding function in  CheckAllRules/TaskAnalyzer.java file. The input to that file is a multitask Rapid program consists of two or more tasks (Each "TASK1" is Robot1 ,"TASK2" is Robot2 ,"TASK3" is Robot3 ,"TASK4" is Robot4) which is seperated by using BEGINTASK-ENDTASK commands. We need to check whether the RULES are satisfied or not . Rules are nothing but whether there exists some Wait instructions and Sync instruction in a particular order around the same set of shared variables in ALL the 4 Robots. There are totally 7 rules to check. Implemented one(Rule 1(a) using WaitSyncTask instruction and Rule 1(b) using SyncMove instruction). It works fine. So as an output we need the set of shared variables in all the tasks, and check whether the Wait instruction is placed in the correct order as specified in the Rule in both the tasks. Finally, output the results like the multitask program has an ERROR or not. If you compile the already given project, you will understand how all the rules are working. I'm attaching examples  here to understand the rules, I also attaching the same examples as seperate input files(name of each input file is according to the rules) along with the project.So you can pick the files directly from there ( In the "InputFiles" folder).




RULES IMPLEMENTED in the project are :
Rule 1(a):- 
        Check for All the Robots whether there is a WaitSyncTask instruction in the first task after the updation of all the shared variables, and before the updation of the same set of shared variables in the other tasks. Also we check that whether for a WaitSyncTask called out , there exists a VAR syncident or not . And we check that there is no duplication of WaitSync calls or there isnt any PERS "task" variable which doesn't exist in the globalTasklist , but is used for a WaitSync call .  These all conditions of WaitSync should be same in each of the corresponding calls according to the Robots of that particular PERS "task" in globalTasklist.
Rule 1(b):- 
        Check for All the Robots whether there is a SyncMove block instruction in the first task after the updation of all the shared variables, and before the updation of the same set of shared variables in the other tasks. Also we check that whether for a SyncMove block called out , there exists a VAR syncident or not corresponding to the syncident used for SyncMoveOn and SyncMoveOff. And we check that there is no duplication or NESTING of SyncMove  calls or there isnt any PERS "task" variable which doesn't exist in the globalTasklist , but is used for a WaitSync call . Also the syncident variable of SyncMoveOn and SyncMoveOff of a SyncMove block must not be same and the order of the id of MOVE commands in  between them should be the same. These all conditions of SyncMove block should be same in each of the corresponding calls according to the Robots of that particular PERS "task" .
Rule 2:- 
        Check whether there is a WaitUntilTestAndSet(consider as a lock) instruction along with a boolean variable  before  the updation of all the shared variables and the same boolean variable is set to false (consider as an unlock)after  the updation of shared variables  in both the tasks.
Rule 3:-
        Check whether there is a boolean variable that is set to true  in the first task before the updation of all the shared variables, and there is a WaitUntil instruction with the same boolean variable before the updation of the same set of shared variables in the second task.
Rule 4:-
        Check whether there is a SETDO instruction with a digital signal(eg.do1) after the updation of all the shared variables in the first task, and there is an ISignalDO instruction with the same digital output (eg.do1) before the updation of all shared variables in the second task.
Rule 5:-
        Check whether there is a SETDO instruction with a digital signal(eg.do1) in the first task after the updation of all  the shared variables, and a WaitDO instruction with the same digital signal(eg.do1)before the updation of the same set of shared variables in the second task.
Rule 6:-
        There is a global variable as string is shared in both the tasks using PERS and in the first task after updation of all the shared variables call a procedure in the second task using that routine string, and check whether the corresponding  procedure is defined in the second task and that procedure uses the shared variables as in the first task.
Rule 7:-
    Check whether there is a set of shared variables in both the tasks and check whether in the second task the set of shared variables are declared as a trap routine inside an IEnable-IDisable block inside main.




ASSUMPTIONS :-
1. The Robot names should be of the form "T_ROB1","T_ROB2","T_ROB3"and "T_ROB4" .
2. The PERS task names should be of the form "task1","task2",etc.
3. The input file of RAPID code should be of the form RObot1->RObot2->RObot3->RObot4


EXAMPLES :-
Rule 1:- 
        Check whether there is a WaitSyncTask instruction in the first task after the updation of all the shared variables, and before the updation of the same set of shared variables in the second task.


BEGINTASK<Task1, Null>
        MODULE Module1
        CONST robtarget Target_10:=[[326.494, 0, 634.740], [0.104, 0, 0.983, 0], [-1, 0, -1, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
        CONST robtarget Target_20:=[[474.642, 0, 298.999], [0.087, 0, 0.996, 0], [-1, 0, 0, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
        CONST robtarget Target_30:=[[17.446, 0, 764.740], [0.809, 0, 0.587, 0], [0, -1, 0, 4], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
        PERS bool obstacle:=FALSE;
        PERS tasks tasklist{2}:=[["Task1"],["Task2"]];
        VAR syncident sync1;
        PROC MAIN()
                IF do1=1 THEN
                    obstacle:=TRUE;
                    WaitSyncTask sync1,tasklist;
                    Path_backward;
                ELSE
                    Path_forward;
                ENDIF
        ENDPROC
        PROC Path_forward()
                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
                MoveJ Target_20,v1000,z100,MyTool\WObj:=wobj0;
                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
        ENDPROC
        PROC Path_backward()
                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
                MoveJ Target_30,v1000,z100,MyTool\WObj:=wobj0;
                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
        ENDPROC
        ENDMODULE
ENDTASK


BEGINTASK<Task2, Null>
        MODULE Module1
        CONST robtarget Target_10:=[[195.6535, -502.4544, 902.740], [0.617, 0, 0.786, 0], [-1, 0, -1, 4], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
        CONST robtarget Target_20:=[[576.642, -502.4544, 408.999], [0.087, 0, 0.996, 0], [-1, 0, 0, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
        CONST robtarget Target_30:=[[-234.446, -502.4544, 880.740], [0.868, 0, 0.495, 0], [-1, 0, -1, 4], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
        PERS bool obstacle:=FALSE;
        PERS tasks tasklist{2}:=[["Task1"],["Task2"]];
        VAR syncident sync1;
        PROC MAIN()
                WaitSyncTask sync1,tasklist;
                IF obstacle=FALSE THEN
                    Path_forward;
                ELSE
                    Path_backward;
                ENDIF
        ENDPROC
        PROC Path_forward()
                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
                MoveJ Target_20,v1000,z100,MyTool\WObj:=wobj0;
                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
        ENDPROC
        PROC Path_backward()
                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
                MoveJ Target_30,v1000,z100,MyTool\WObj:=wobj0;
                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
        ENDPROC
        ENDMODULE
ENDTASK


Rule 2:- 
        Check whether there is a WaitUntilTestAndSet(consider as a lock) instruction along with a boolean variable  before the updation of all the shared variables and the same boolean variable is set to false (consider as an unlock)after the updation of shared variables  in both the tasks.


Eg:-


BEGINTASK<Task1, Null>
1        MODULE Module1
2        CONST robtarget Target_10:=[[326.494, 425, 634.740], [0.104, 0, 0.983, 0], [-1, 0, -1, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
3        CONST robtarget Target_20:=[[-474.642, 265, 298.999], [0.087, 0, 0.996, 0], [-1, 0, 0, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
4        CONST robtarget Initial_point:=[[0.446, 0, 764.740], [0.809, 0, 0.587, 0], [0, -1, 0, 4], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
5        PERS bool tproutine_inuse:=FALSE;
5        PROC MAIN()
6                WaitUntil TestAndSet(tproutine_inuse);
7                IF Target_10.trans.x>0 and Target_20.trans.x<0
8                    Path_Q1_Q2;
9                tproutine_inuse:=FALSE;
10        ENDPROC
11        PROC Path_Q1_Q2()
12                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
13                MoveJ Target_20,v1000,z100,MyTool\WObj:=wobj0;
14                MoveJ Initial_point,v1000,z100,MyTool\WObj:=wobj0;
15        ENDPROC
16         ENDMODULE
ENDTASK                


BEGINTASK<Task2, Null>
1        MODULE Module1
2        PERS robtarget Target_10;
3        PERS robtarget Target_20;
4        PERS bool tproutine_inuse:=FALSE;
5        PROC MAIN()
6                WaitUntil TestAndSet(tproutine_inuse);
7                    Target_10.trans.x:=0;
8                    Target_20.trans.x:=0;
9                    tproutine_inuse:=FALSE;
10        ENDPROC
11        ENDMODULE
ENDTASK                




Rule 3:-
        Check whether there is a boolean variable that is set to true  in the first task before the updation of all the shared variables, and there is a WaitUntil instruction with the same boolean variable before the updation of the same set of shared variables in the second task.


Eg:-


BEGINTASK<Task1, Null>
1        MODULE Module1
2        CONST robtarget Target_10:=[[326.494, 0, 634.740], [0.104, 0, 0.983, 0], [-1, 0, -1, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
3        CONST robtarget Target_20:=[[474.642, 0, 298.999], [0.087, 0, 0.996, 0], [-1, 0, 0, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
4        CONST robtarget Target_30:=[[17.446, 0, 764.740], [0.809, 0, 0.587, 0], [0, -1, 0, 4], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
5        PERS bool obstacle:=FALSE;
6        PERS bool startsync:=TRUE;
7        PROC MAIN()
8                startsync:=TRUE;
9                IF do1=1 THEN
10                    obstacle:=TRUE;
11                    Path_backward;
12                ELSE
13                    Path_forward;
14                ENDIF
15        ENDPROC
16        PROC Path_forward()
17                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
18                MoveJ Target_20,v1000,z100,MyTool\WObj:=wobj0;
19                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
20        ENDPROC
21        PROC Path_backward()
22                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
23                MoveJ Target_30,v1000,z100,MyTool\WObj:=wobj0;
24                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
25        ENDPROC
26         ENDMODULE
ENDTASK                


BEGINTASK<Task2, Null>
1        MODULE Module1
2        CONST robtarget Target_10:=[[195.6535, -502.4544, 902.740], [0.617, 0, 0.786, 0], [-1, 0, -1, 4], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
3        CONST robtarget Target_20:=[[576.642, -502.4544, 408.999], [0.087, 0, 0.996, 0], [-1, 0, 0, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
4        CONST robtarget Target_30:=[[-234.446, -502.4544, 880.740], [0.868, 0, 0.495, 0], [-1, 0, -1, 4], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
5        PERS bool obstacle:=FALSE;
6        PERS bool startsync;
7        PROC MAIN()
8        WaitUntil startsync;
9                IF obstacle=FALSE THEN
10                    Path_forward;
11                ELSE
12                    Path_backward;
13                ENDIF
14        ENDPROC
15        PROC Path_forward()
16                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
17                MoveJ Target_20,v1000,z100,MyTool\WObj:=wobj0;
18                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
19        ENDPROC
20        PROC Path_backward()
21                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
22                MoveJ Target_30,v1000,z100,MyTool\WObj:=wobj0;
23                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
24        ENDPROC
25        ENDMODULE
ENDTASK                




Rule 4:-
        Check whether there is a SETDO instruction with a digital signal(eg.do1) after the updation of all the shared variables in the first task, and there is an ISignalDO instruction with the same digital output (eg.do1) before the updation of all shared variables in the second task.


Eg:-
BEGINTASK<Task1, Null>
1        MODULE Module1
2        CONST robtarget Target_10:=[[326.494, 425, 634.740], [0.104, 0, 0.983, 0], [-1, 0, -1, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
3        CONST robtarget Target_20:=[[-474.642, 265, 298.999], [0.087, 0, 0.996, 0], [-1, 0, 0, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
4        CONST robtarget Initial_point:=[[0.446, 0, 764.740], [0.809, 0, 0.587, 0], [0, -1, 0, 4], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
5        PROC MAIN()
6                IF Target_10.trans.x>0 and Target_20.trans.x<0
7                    Path_Q1_Q2;
8                SETDO do1,1;
9        ENDPROC
10        PROC Path_Q1_Q2()
11                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
12                MoveJ Target_20,v1000,z100,MyTool\WObj:=wobj0;
13                MoveJ Initial_point,v1000,z100,MyTool\WObj:=wobj0;
14        ENDPROC
15         ENDMODULE
ENDTASK                


BEGINTASK<Task2, Null>
1        MODULE Module1
2        PERS robtarget Target_10;
3        PERS robtarget Target_20;
4        VAR intnum isint1;
5        PROC MAIN()
6                CONNECT isint1 WITH isitrap;
7                ISignalDO do1,1,isint1;
8                    Target_10.trans.x:=0;
9                    Target_20.trans.x:=0;
10                IDelete isint1;
11        ENDPROC
12         TRAP isitrap()
13                TPWrite"Trap executed";
14        ENDTRAP
15        ENDMODULE
ENDTASK                




Rule 5:-
        Check whether there is a SETDO instruction with a digital signal(eg.do1) in the first task after the updation of all the shared variables, and a WaitDO instruction with the same digital signal(eg.do1)before the updation of the same set of shared variables in the second task.


Eg:-


BEGINTASK<Task1, Null>
1        MODULE Module1
2        CONST robtarget Target_10:=[[326.494, 425, 634.740], [0.104, 0, 0.983, 0], [-1, 0, -1, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
3        CONST robtarget Target_20:=[[-474.642, 265, 298.999], [0.087, 0, 0.996, 0], [-1, 0, 0, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
4        CONST robtarget Initial_point:=[[0.446, 0, 764.740], [0.809, 0, 0.587, 0], [0, -1, 0, 4], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
5        PROC MAIN()
6                IF Target_10.trans.x>0 and Target_20.trans.x<0
7                    Path_Q1_Q2;
8                SETDO do1,0;
9        ENDPROC
10        PROC Path_Q1_Q2()
11                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
12                MoveJ Target_20,v1000,z100,MyTool\WObj:=wobj0;
13                MoveJ Initial_point,v1000,z100,MyTool\WObj:=wobj0;
14        ENDPROC
15         ENDMODULE
ENDTASK                


BEGINTASK<Task2, Null>
1        MODULE Module1
2        PERS robtarget Target_10;
3        PERS robtarget Target_20;
4        PROC MAIN()
5                WaitDO do1,0;
6                    Target_10.trans.x:=0;
7                    Target_20.trans.x:=0;
8        ENDPROC
9        ENDMODULE
ENDTASK                


                
Rule 6:-
        There is a global variable as string is shared in both the tasks using PERS and in the first task after updation of all the shared variables call a procedure in the second task using that routine string, and check whether the corresponding procedure is defined in the second task and that procedure uses the shared variables as in the first task.


Eg:-


BEGINTASK<Task1, Null>
1        MODULE Module1
2        CONST robtarget Target_10:=[[326.494, 425, 634.740], [0.104, 0, 0.983, 0], [-1, 0, -1, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
3        CONST robtarget Target_20:=[[-474.642, 265, 298.999], [0.087, 0, 0.996, 0], [-1, 0, 0, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
4        CONST robtarget Initial_point:=[[0.446, 0, 764.740], [0.809, 0, 0.587, 0], [0, -1, 0, 4], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
5        PERS string routine_string:="";
6        PROC MAIN()
7                IF Target_10.trans.x>0 and Target_20.trans.x<0
8                    Path_Q1_Q2;
9                routine_string:="routineback";
10        ENDPROC
11        PROC Path_Q1_Q2()
12                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
13                MoveJ Target_20,v1000,z100,MyTool\WObj:=wobj0;
14                MoveJ Initial_point,v1000,z100,MyTool\WObj:=wobj0;
15        ENDPROC
16         ENDMODULE
ENDTASK                


BEGINTASK<Task2, Null>
1        MODULE Module1
2        PERS robtarget Target_10;
3        PERS robtarget Target_20;
4        PERS string routine_string:="";
5        PROC MAIN()
6                routine_back;
7        ENDPROC
8        PROC routine_back()
9                    Target_10.trans.x:=0;
10                    Target_20.trans.x:=0;
11        ENDPROC
12        ENDMODULE
ENDTASK                




Rule 7:-
Check whether there is a set of shared variables in both the tasks and check whether in the second task the set of shared variables are declared as a trap routine inside an IEnable-IDisable block inside main.




BEGINTASK<Task1, Null>
1        MODULE Module1
2        CONST robtarget Target_10 :=[[326.494, 425, 634.740], [0.104, 0, 0.983, 0], [-1, 0, -1, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
3        CONST robtarget Target_20 :=[[-474.642, 265, 298.999], [0.087, 0, 0.996, 0], [-1, 0, 0, 0], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
4        CONST robtarget Initial_point :=[[0.446, 0, 764.740], [0.809, 0, 0.587, 0], [0, -1, 0, 4], [9E+09, 9E+09, 9E+09, 9E+09, 9E+09, 9E+09]];
5        PROC MAIN()
6                IF Target_10.trans.x>0 and Target_20.trans.x<0
7                    Path_Q1_Q2;
8        ENDPROC
9        PROC Path_Q1_Q2()
10                MoveJ Target_10,v1000,z100,MyTool\WObj:=wobj0;
11                MoveJ Target_20,v1000,z100,MyTool\WObj:=wobj0;
12                MoveJ Initial_point,v1000,z100,MyTool\WObj:=wobj0;
13        ENDPROC
14         ENDMODULE
ENDTASK                


BEGINTASK<Task2, Null>
1        MODULE Module1
2        PERS robtarget Target_10 ;
3        PERS robtarget Target_20 ;
5        VAR intnum int1;
5        PROC MAIN()
6                IEnable;
7                CONNECT int1 WITH backroutine;
8                IDisable;
9        ENDPROC
10        TRAP backroutine
11                    Target_10.trans.x:=0;
12                    Target_20.trans.x:=0;
13        ENDTRAP
14        ENDMODULE
ENDTASK