# PHP Runtime Source
This directory contains two files only, the bootstrap scrip and a binary PHP executable which was compiled using the automated builder.

The bootstrap script (doesn't have to be in PHP) simply runs an infinite loop that keeps checking for new invocation requests from the Amazon Lambda Runtime API. Once a new request is received, it calls the `handler` function with the payload as a single parameter to that function and expects a response array which then is encoded into JSON format and sent to the Lambda Runtime API. Then the same process repeats.