
---
layout: post
title: Basics of Ruby
date: 2022-08-12 13:32:20 +0300
description: Ruby language basics
img: icons/document.svg
fig-caption: test caption # Add figcaption (optional)
tags: [Ruby]
---

# Ruby Notes

## Setup

- Use Irb Prompt To Debug On Ssh Box 
	- Irb Then Typing Statements Or Irb Scriptfile.Rb  
- Running File On Mac:
	- Create Xyz.Rb File - Add Shebang (#!/Usr/Bin/Env Ruby) To Specify Interpreter - Type ./Xyz.Rb To Run
- Everything In Ruby Is An Object: Including Numbers 

## Basics 

- Local Var : V = 1, Global Var: $V = 1, Instance Var: @V =1, Class Var: @@V = 1
	- Also Can Turn "Hello" String To :Hello Symbol By "Hello".To_Sym And Use It Like Print :Hello.To_S 
- Can Do Alias For Vars: Alias $A $B
- Constants Must Being With Capital Letter: Myvar = 1 Or Myvar = 1
	- Unlike Other Langs, Consts Are Objects So Mutable, But Don't Do That

## Ranges 
- (1..9) Is 1 To 9(Included)
- (1...9) Is 1 To 9(Excluded)
- (1..9) == 8 For Existence Check
- (1..9).To_A: To Convert Into Array [1,2,3....9]
  
### Method:
- Def Methodname(P1,P2) End 
-  Call: Methodname(P1,P2) Or Methodname P1 P2
- Object Method Call: Obj.Method Or Obj#Method Or Obj::Method
- Send Entire Function As Param: Def Funca(&Funcb): Funcb.Call(Xyz)
- Name Ending Conventions:
	-  End With ? Def Method?: Will Mostly Return Bool
	- Ends With !: Changes The Input Object 
	- Ends With =: Sets Up Assignment
- Default Arguments: Def Method(P1:"Default_Val") Or Def Method(P1="Default_Val") 
- Variable No Of Arguments: Def Method(A,B,*Args): Args.Size Etc 

### Blocks:
- Block Is A Nameless Function That Can Be Passed Around
- Array.Each Someblock: Here Someblock Could Be {|Elm| Print Elm} Or Do |Elm| Print Elm End
- You Can Send Block To A Function That Has Yield, The Function Will Run The Block 
	- `Def Myfun: Yield`, 
	- Call Like This: `Myfun <Block>` , I.E. `Myfun {Puts "Something"}`
### Procs
- Like Blocks But Named
- `Myproc = Proc.New {Somecode}` Or Lambda {Soemcode} Or ->{Somecode} Or Proc {Somecode}
- Calling: `Myproc.Call` : Executes The Code Inside Proc
- `Def Myfun(&Someproc)`: Yield Can Accept Proc As Function Arg Bcoz We Had & Prefix
- Conditionals: If Test Something Elsif Something End 
- Use `Begin {Code}` And `End{Code}` To Run Something Before And After The File Code Is Run

## Classes
Ruby Supports Single Inheritence 

    Class Myclass End
     Def Initialize(): 
       @Varname = 1
    M = Myclass.New()
    M.Somefunction()

### Accessors:
   - Attr :Bark, True : Sets Getter And Setter For Bark I.E. Class.Bark = X, Print Class.Bark
   - Attr_Reader :Bark: Sets Getter
   - Attr_Writter :Bark: Sets Setter
   - Attr_Accessor :Bark: Sets Getter & Setter Both

- @Var Is Instance Variable: Unique Among Each Instance
- @@Var Is Class Variable: Shared Across Instances 
- Static Methods: Prefix Method Definitions With `Self.Methodname` Or `Class.Methodname` To Make It Static I.E. `Def Self.Run()`
- Inheritence : `Class Child < Parent` To Create Child Classes

## Misc
- Try Begin End 
- Catch Becomes Rescue
- Finally Becomes Ensure
``` 
Begin
Somefunction()
Rescue Ioerror
Puts "Some Error"
Ensure
Closeconnection()
End 
```
                                    
- Can Also Use Raise `Errortype`, "`Errmessage`" To Throw An Error
