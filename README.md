# Churn-emails-using-Python
In this project, i am going to showcase how to read, sort, count and to do many such things using Python programming language.

To have access to your emails using Python or web console or Linux system, export your mailbox data in .Py, or .txt or excel or .html or .json format and store it in your system or upload it to the jupyter notebook. Emails can be accessed either with the file name or file path in your system

Let's see how and what can be done with just our mailbox:

# Dataset
I have a text file which records mail activity from various individuals in an open source project development team. Use the web console or Linux system or Jupyter Notebook to open the file. Below is the file location

cat /cxldata/datasets/project/mbox-short.txt

The above code allows you to read emails of your inbox.
To see the first 15 lines or last 5 lines of mbox-short.txt, use below command on the console

head -n 15 /cxldata/datasets/project/mbox-short.txt

tail -n 15 /cxldata/datasets/project/mbox-short.txt

These files are in a standard format for a file containing multiple mail messages. The lines which start with "From " separate the messages and the lines which start with "From:" are part of the messages.

# Count the Number of Lines
If we know the file is relatively small compared to the size of our main memory, we can read the whole file into one string using the read method on the file handle. Example -

fhand = open('/cxldata/datasets/project/mbox-short.txt') 
inp = fhand.read()
print(inp)

INSTRUCTIONS

- Define a function number_of_lines
- Open the file mbox-short.txt which is located at /cxldata/datasets/project/mbox-short.txt
- Read the file into one string by using read method on file handle
- Write logic to count the number of lines
- Return the count of the number of lines

fhand = open('/cxldata/datasets/project/mbox-short.txt')
count = 0
for lines in fhand:
    count = count+1
print("number_of_lines:",count)


So, the above code shows there are 1910 number of lines in my mailbox.

# Count the Number of Subject Lines
We use the string method startswith to select only those lines with the desired prefix.

The below code prints the lines starting with From:

fhand = open('/cxldata/datasets/project/mbox-short.txt') 
count = 0 
for line in fhand: 
    line = line.rstrip() # Remove new line characters from right
    if line.startswith('From:'):
        print(line)


INSTRUCTIONS

Write a function count_number_of_lines which returns the count of the number of lines starting with Subject: in the file /cxldata/datasets/project/mbox-short.txt

def count_number_of_lines():
    with open('/cxldata/datasets/project/mbox-short.txt') as f:
        count = 0
        for line in f:
            line = line.rstrip() # Remove new line characters from right
            if line.startswith('Subject:'):
                count = count + 1
    return count
count_number_of_lines()


# Find Average Spam Confidence
In the above exercise, we saw a couple of examples of startswith. Let's do one more hands-on with startswith

INSTRUCTIONS

- Define a function average_spam_confidence which calculates the average spam confidence and returns it
- Open the file mbox-short.txt which is located at /cxldata/datasets/project/mbox-short.txt
- Loop through the file handle
- Select only those lines starts with X-DSPAM-Confidence:
- Split the lines at : and take the float value which is spam confidence
- Find the average of this spam confidence in the entire file and return it.

def average_spam_confidence():
    file=open("/cxldata/datasets/project/mbox-short.txt")
    TotalSum=0.0
    count=0;
    for line in file:        
        if(line.startswith("X-DSPAM-Confidence:")):
            count=count+1
            line=line.rstrip()
            TotalSum+=float(line.split(':')[1].strip())
    AverageSpam=float(TotalSum/float(count))
    return AverageSpam
average_spam_confidence()


# Find Which Day of the Week the Email was sent

Write a function find_email_sent_days which reads the file /cxldata/datasets/project/mbox-short.txt and categorizes each mail message by which day of the week the email was sent.
To do this do the following:

- Open the file and read it line by line
- Look for lines that start with "From"
- For those lines which start from "From", then look for the third word and keep a running count of each of the days of the week.

Note: You have to store the results in a dictionary. Only store those day of the week that exists. For Example, if there is no line for Mon then it should not be in the dictionary elements.

- At the end of the program return the contents of your dictionary.

def find_email_sent_days():
    fhand=open('/cxldata/datasets/project/mbox-short.txt')
    daydict={}
    for line in fhand:
        line =line.rstrip()
        if line.startswith('From'):
            sline= line.split()
            if len(sline)>2:
                day=sline[2]
                daydict[day]=daydict.get(day,0)+1
    return daydict
find_email_sent_days()


# Count Number of Messages From Each Email Address
Write a function count_message_from_email which reads the file /cxldata/datasets/project/mbox-short.txt.

This function builds a histogram using a dictionary to count how many messages have come from each email address and returns the dictionary.

def count_message_from_email():
    lineslist=[]
    emaildict={}
    with open("/cxldata/datasets/project/mbox-short.txt") as f:
        for line in f:
            lineslist = line.split()
            if line.startswith('From:'):
                email=lineslist[1]
                if email not in emaildict:
                    emaildict[email] = 1
                else:
                    emaildict[email] += 1
    return emaildict
print(count_message_from_email())


# Count Number of Messages From Each Domain
Write a function count_message_from_domain which reads the file /cxldata/datasets/project/mbox-short.txt.

This function builds a histogram using a dictionary to count how many messages have come from each domain(Instead of from email address), and returns the dictionary.

def count_message_from_domain():
    fhand = open('/cxldata/datasets/project/mbox-short.txt')
    domaincount={}
    for line in fhand:
        line=line.rstrip()
        if line.startswith("From:"):
            for line1 in line.split():
                if '@' in line1:
                    y=slice(line1.find('@')+1,len(line1))
                    domaincount[line1[y]]=domaincount.get(line1[y],0)+1
    return domaincount
count_message_from_domain()


This way, even you can play with your mailbox and get some valuable information whenever required, without spending too much time to check each individual mail.

If you like it, hit clap and please provide your valuable feedback.

Thanks!
