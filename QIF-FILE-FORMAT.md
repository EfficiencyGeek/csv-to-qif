# QIF File Format

https://www.w3.org/2000/10/swap/pim/qif-doc/QIF-doc.htm#:~:text=A%3A%20The%20Quicken%20interchange%20format,that%20supports%20the%20QIF%20format.

Q: What is the Quicken interchange format (QIF)?
A: The Quicken interchange format (QIF) is a specially formatted text (ASCII) file that lets you to move Quicken transactions:
From one Quicken account register into another Quicken account register, or
To/From another application that supports the QIF format.
Note: For Quicken to translate data from a text file into the Quicken register as transactions, the text file must be in the QIF format.
Required File Formatting:
Each transaction must end with a symbol, indicating the end of entry.
Each item in the transaction must display on a separate line.
When Quicken exports an account register or list, it adds a line to the top of the file that identifies the type of account or list. Listed below are the header lines Quicken adds to the exported files:
Header	Type of data
!Type:Bank	Bank account transactions
!Type:Cash	Cash account transactions
!Type:CCard	Credit card account transactions
!Type:Invst	Investment account transactions
!Type:Oth A	Asset account transactions
!Type:Oth L	Liability account transactions
!Account	Account list or which account follows
!Type:Cat	Category list
!Type:Class	Class list
!Type:Memorized	Memorized transaction list
You can force Quicken to import all transfers, regardless of whether Ignore Transfers is selected when the file is imported. You must add a line to the file being imported into a Quicken account. Use a text editor or word processor to put the following line right after the header line at the top of the file:
!Option:AllXfr
Items for Non-Investment Accounts

Each item in a bank, cash, credit card, other liability, or other asset account must begin with a letter that indicates the field in the Quicken register. The non-split items can be in any sequence:
Field	Indicator Explanation
D	Date
T	Amount
C	Cleared status
N	Num (check or reference number)
P	Payee
M	Memo
A	Address (up to five lines; the sixth line is an optional message)
L	Category (Category/Subcategory/Transfer/Class)
S	Category in split (Category/Transfer/Class)
E	Memo in split
$	Dollar amount of split
^	End of the entry
Note: Repeat the S, E, and $ lines as many times as needed for additional items in a split. If an item is omitted from the transaction in the QIF file, Quicken treats it as a blank item.
Items for Investment Accounts

Field	Indicator Explanation
D	Date
N	Action
Y	Security
I	Price
Q	Quantity (number of shares or split ratio)
T	Transaction amount
C	Cleared status
P	Text in the first line for transfers and reminders
M	Memo
O	Commission
L	Account for the transfer
$	Amount transferred
^	End of the entry
Items for Account Information

The account header !Account is used in two places-at the start of an account list and the start of a list of transactions to specify to which account they belong.
Field	Indicator Explanation
N	Name
T	Type of account
D	Description
L	Credit limit (only for credit card accounts)
/	Statement balance date
$	Statement balance amount
^	End of entry
Items for a Category List

Field	Indicator Explanation
N	Category name:subcategory name
D	Description
T	Tax related if included, not tax related if omitted
I	Income category
E	Expense category (if category type is unspecified, quicken assumes expense type)
B	Budget amount (only in a Budget Amounts QIF file)
R	Tax schedule information
^	End of entry
Items for a Class List

Field	Indicator Explanation
N	Class name
D	Description
^	End of entry
Items for a Memorized Transaction List

Immediately preceding the ^ character, each entry must end with one of the following file indicators to specify the transaction type.
KC
KD
KP
KI
KE
With that exception, memorized transaction entries have the same format as regular transaction entries (non-investment accounts). However, the Date or Num field is included. All items are optional, but if an amortization record is included, all seven amortization lines must also be included.
Field	Indicator Explanation
KC	Check transaction
KD	Deposit transaction
KP	Payment transaction
KI	Investment transaction
KE	Electronic payee transaction
T	Amount
C	Cleared status
P	Payee
M	Memo
A	Address
L	Category or Transfer/Class
S	Category/class in split
E	Memo in split
$	Dollar amount of split
1	Amortization: First payment date
2	Amortization: Total years for loan
3	Amortization: Number of payments already made
4	Amortization: Number of periods per year
5	Amortization: Interest rate
6	Amortization: Current loan balance
7	Amortization: Original loan amount
^	End of entry
Examples of QIF files

Normal Transactions Example

Transaction Item	Comment (not in file)
!Type:Bank	Header
D6/ 1/94	Date
T-1,000.00	Amount
N1005	Check number
PBank Of Mortgage	Payee
L[linda]	Category
S[linda]	First category in split
$-253.64	First amount in split
SMort Int	Second category in split
$-746.36	Second amount in split
^	End of the transaction
D6/ 2/94	Date
T75.00	Amount
PDeposit	Payee
^	End of the transaction
D6/ 3/94	Date
T-10.00	Amount
PJoBob Biggs	Payee
MJ.B. gets bucks	Memo
LEntertain	Category
A1010 Rodeo Dr.	Address (line 1)
AWaco, Tx	Address (line 2)
A80505	Address (line 3)
A	Address (line 4)
A	Address (line 5)
A	Address (line 6)
^	End of the transaction
Investment Example

Transaction Item	Comment (not in file)
!Type:Invst	Header line
D8/25/93	Date
NShrsIn	Action (optional)
Yibm4	Security
I11.260	Price
Q88.81	Quantity
CX	Cleared Status
T1,000.00	Amount
MOpening	Balance Memo
^	End of the transaction
D8/25/93	Date
NBuyX	Action
Yibm4	Security
I11.030	Price
Q9.066	Quantity
T100.00	Amount
MEst. price as of 8/25/93	Memo
L[CHECKING]	Account for transfer
$100.00	Amount transferred
^	End of the transaction
Memorized List Example

Transaction Item	Comment (not in file)
!Type:Memorized	Header line
T-50.00	Amount
PJoe Hayes	Payee
MRent	Memo
KC	Check transaction
^	End of the transaction
T-25.00	Amount
T-25.00	Company Payee
LTelephone	Category
KP	Payment transaction
^	End of the transaction
