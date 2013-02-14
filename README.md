Luhn-Algo-Js
============
  Here are some information for doing credit card number validation:
  1. First digit of credit card number is the Major Industry Identifier (MII)
     which represents the category of entity which issued your credit card

     Different MII digits represent the following issuer categories:

  	0	ISO/TC 68 and other industry assignments
		1	Airlines
		2	Airlines and other industry assignments
		3	Travel and entertainment
		4	Banking and financial
		5	Banking and financial
		6	Merchandizing and banking
		7	Petroleum
		8	Telecommunications and other industry assignments
		9	National assignment

     For example, my VISA credit card number started with number 4 means, VISA is card
     issuer of Banking & Financial category. 

  2. First 6 digit of credit card (including that MII above) form an issuer identifier.
     Having 6 digit means we have 10^6 or 1.000.000 total number of possible credit card
     issuers. Some of the better known issuer identifiers are:
	- Diner's Club/Carte Blanche
	   * credit card number format is 300xxx-305xxx, 36xxxx, or 38xxxx
	     with card number length 14
	- American Express
	   * credit card number format is 34xxxx, 37xxxx with card number length is 15
	- VISA
	   * credit card number format is 4xxxxx, with card number length is 13 or 16
	- MasterCard
	   * credit card number format is 51xxxx-55xxxx, with card number length is 16
	- Discover
	   * credit card number format is 6011xx, with card number length is 16

  3. The rest digit started from digit no. 7 until (n-1) where n is the length of credit
     card number, is our account number. The last digit is a check digit. 

     Maximum length of credit card number is 19 digit, means maximum number of account
     number is 12 digit (remember that first 6 digit is issuer identifier & last digit is
     check digit).

     So having 12 digit account number means each card issuer could have 10^12 or
     1.000.000.000.000 account number.

  4. The last digit is check digit, to calculate this check digit we use Luhn Algorithm
     This algorithm is also known as modula10 or mod10 algorithm

  Example:
  What is card type, issuer identifier and check if this card number is valid
    4408 0412 3456 7890

  Solution:
  1. Prefix 4xxxxx -> this card is VISA
  2. Issuer Identifier: 440804
  3. Account number   : 123456789
  4. Run Luhn Algo to check if card number valid
     Step 1:
       Double the alternate digits starting from the first digit.
       From card number:
	   4408 0412 3456 7890
           ^ ^  ^ ^  ^ ^  ^ ^  --> to double on step 1

       (4+4) (0+0) (0+0) (1+1) (3+3) (5+5) (7+7) (9+9)
         8     0     0     2     6     10    14    18

     Step 2:
        For each result of step 1, if the value is bigger than
	9 we need to substract by 9 so each value is less than 10.
	After that we append all of them

        8     0     0     2     6     10    14    18
	                               ^     ^     ^ --> need to substract by 9

        Hence we have:

	8  +  0  +  0  +  2  +  6  +  1  +  5  +  9 = 31

     Step 3:
        Now add all the non-doubled digits from the credit card number
        From card number:
	  4408 0412 3456 7890
           ^ ^  ^ ^  ^ ^  ^ ^ --> to process on step 3

	   Hence we have: 4 + 8 + 4 + 2 + 4 + 6 + 8 + 0 = 36

      Step 4:
       Add the values calculated in step 2 and step 3 together
       We have 31+36 = 67

      Step 5 :
        Take the value calculated in step 4 and calculate the remainder when it is
	divided by 10. If the remainder is zero, then it's a valid number, otherwise
	it's invalid.

	So we have 67 % 10, reminder is 7 not 0 means this card number is invalid

      If we change the check digit to 3 we will have on step 3 values 39 and hence we have
      70 on step 4 and 70 % 0 -> reminder is 0 -> means card number is valid.

  Implementation in JavaScript (HTML included, just copy paste, save as HTML and run it on browser).
