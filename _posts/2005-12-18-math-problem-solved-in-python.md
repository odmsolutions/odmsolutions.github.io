---
layout: post
description: Math Problem Solved in Python
tags: [python,programming]
title: Math Problem Solved in Python
---
{% include JB/setup %}

I use the Python programming language, and came across a mathematics problem in an oldish (July 2005) copy of News Scientist.

The problem (number 1343 in their regular enigma column) was this:
* Find the largest whole number
* whose digits are different
* do not include 0
* that is divisible by all of its individual digits.

After playing with it, and reading around a little, I came up with a small python script which could solve the problem in 10 to 15 seconds on my machine - and that is not on an unused machine.

# Some notes on my assumptions

As any even number x 5 make a 10, which would not be allowable because of the 0 rule, the number probably does not include a 5. This assumption, which reduces the possibilities vastly is used throughout the code.

The code uses a string form of the number quite extensively since the digits are so important here. The skipnumberatindex function is not as clean as I would like - but it does what it is supposed to well.

So - here is my code:

    def has_repeating_number(numstr):
      for digit in numstr:
        first = numstr.find(digit)
        next = numstr.find(digit,first+1)
        if(next != -1):
          return (True, next)
      return (False, -1)

    def can_be_divided_by_digits(number,numstr):
      for digstr in numstr:
        if number % int(digstr) &gt; 0:
          return False;
      return True;

    #This base number saves going through the repeat and 
    #other tests when you have subtracted one from an inner
    #number. An earlier version set the digits after to 9's

    basenumberstr = "98764321"

    def skipnumberatindex(index, number, numstr):
        #skip the complex stuff if it is merely enough to subtract 1
        if index == len(numstr) - 1:
                return number - 1

        digit = numstr[index]
        while digit=='0':
                index -= 1
                digit = numstr[index]

        digitminusone = str(int(digit)-1)

        rindex = (len(numstr) - index) - 1

        outnumstr = (numstr[:index],
                digitminusone,
                basenumberstr[:rindex])
        outnumstr = ''.join(outnumstr)
        return int(outnumstr)

    #I have started at the following number for some good 
    #reasons.  Since we can only have one of each digit, and
    #that none of them are 5, or 0, then we can only have 8
    #digits. Since we are going for the largest number,
    #then the digits are present in descending order

    currentnumber = 98764321

    while currentnumber &gt; 0:
        currentnumber -= 1
        numstr = str(currentnumber)
        #Skip zeros
        if (currentnumber % 10 == 0) or (currentnumber % 5 == 0):
                currentnumber -= 1;
        elif '0' in numstr:
                #Get the place of zero in the number, from the right
                currentnumber = skipnumberatindex(numstr.find('0'), currentnumber, numstr)
        elif '5' in numstr:
                #Get the place of a five in the number
                currentnumber = skipnumberatindex(numstr.find('5'), currentnumber, numstr)
        else:
                (hasrepeat, where) = has_repeating_number(numstr)
                if hasrepeat:
                        #Okay - reverse the where a little
                        currentnumber = skipnumberatindex(where, currentnumber, numstr)
                elif not can_be_divided_by_digits(currentnumber,numstr):
                        currentnumber -= 1
                else:
                        break

    print "Number should be %s\n" % (str(currentnumber))

If you have any comments or further optimisations, please let me know!

