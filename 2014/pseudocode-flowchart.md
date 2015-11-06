@(Cabinet)[coding_assist|published]

# Pseudocode, Code and Flowchart

In machine learning community, the code is usually not very long and somewhat sloppy. However, when things are getting complicated and we want to maintain the code, we may need to make our code more friendly and readable. But how?

Jeff Atwood argues in Pseudocode or Code that writing pseudocode before actually coding is impractical. Personally, I don’t agree.

Quoted from Pseudocode or Code:

So if we we set out to write an error handling lookup routine, we’d first write it in pseudocode:
set the default status to "fail"
look up the message based on the error code
```
if the error code is valid
    if doing interactive processing, display the error message
        interactively and declare success
    if doing command line processing, log the error message to the
        command line and declare success
if the error code isn't valid, notify the user that an
    internal error has been detected
return status information
```
Then, when you’re satisfied that you understand what the routine should do, you turn that pseudocode into comments that describe the code you’re about to write.
```
// set the default status to "fail"
Status errorMessageStatus = Status_Failure;

// look up the message based on the error code
Message errorMessage = LookupErrorMessage( errorToReport );

// if the error code is valid
if ( errorMessage.ValidCode() ) {

// determine the processing method
    ProcessingMethod errorProcessingMethod = CurrentProcessingMethod();

// if doing interactive processing, display the error message
// interactively and declare success
    if ( errorProcessingMethod == ProcessingMethod_Interactive ) {
        DisplayInteractiveMessage( errorMessage.Text() );
        errorMessageStatus = Status_Success;
    }
```
Pseudocode is sort of like the Tang of programming languages — you hydrate the code around it.
As someone says, pseudocode is not about writing down precisely what should happen but a general idea of what should happen— an overall view. After this, the pseeudocode can be part of the comments. 

According to **Code Complete**, the guidelines for using pseudocode effectively are as follows:

Use English-like statements that precisely describe specific operations.
Avoid syntactic elements from the target programming language. Pseudocode allows you to design at a slightly higher level than the code itself. When you use programming-language constructs, you sink to a lower level, eliminating the main benefit of design at a higher level, and you saddle yourself with unnecessary syntactic restrictions.
Write pseudocode at the level of intent. Describe the meaning of the approach rather than how the approach will be implemented in the target language.
Write pseudocode at a low enough level that generating code from it will be nearly automatic. If the pseudocode is at too high a level, it can gloss over problematic details in the code. Refine the pseudocode in more and more detail until it seems as if it would be easier to simply write the code.