# csvhead

So you're deep into processing lots of data. Someone sent you an export of customer orders, or you have a list of inventory for thousands of products. You have no idea what's in these files, let alone what to do with them.

`csvhead` to the rescue.

This simple script lets you preview the CSV. It shows column numbers, column names, and sample values from the first row.

```
$ cat test.csv | head -n2
"Lastname","Firstname","SSN","Test1","Test2","Test3","Test4","Final","Grade"
"Alfalfa","Aloysius","123-45-6789",40.0,90.0,100.0,83.0,49.0,"D-"

$ cat test.csv | csvhead
    1 Lastname    (Alfalfa)
    2 Firstname   (Aloysius)
    3 SSN         (123-45-6789)
    4 Test1       (40.0)
    5 Test2       (90.0)
    6 Test3       (100.0)
    7 Test4       (83.0)
    8 Final       (49.0)
    9 Grade       (D-)
```

### Other delimiters

Maybe you have a pipe separated file instead? No problem. Just pass the delimeter character as the first argument to `csvhead`.

```
$ cat test.psv | head -n2
"Lastname"|"Firstname"|"SSN"|"Test1"|"Test2"|"Test3"|"Test4"|"Final"|"Grade"
"Alfalfa"|"Aloysius"|"123-45-6789"|40.0|90.0|100.0|83.0|49.0|"D-"

$ cat test.psv | csvhead '|'
    1 Lastname    (Alfalfa)
    2 Firstname   (Aloysius)
    3 SSN         (123-45-6789)
    4 Test1       (40.0)
    5 Test2       (90.0)
    6 Test3       (100.0)
    7 Test4       (83.0)
    8 Final       (49.0)
    9 Grade       (D-)
```

## How to install

Just copy the script below into a file that's executable.

```
pbpaste > ~/csvhead
chmod a+x ~/csvhead
```

You'll want to make sure this file lives in your `PATH` if you plan on using it frequently.

## Combine with `csvfix` for real magic

One of the most underrated tools out there is [csvfix](https://neilb.bitbucket.io/csvfix/manual/csvfix16/csvfix.html?Usage.html). It's like a Swiss Army knife for CSV files. Combine it with `csvhead` if you really want to up your command line CSV game.

#### Use `csvhead` to get column names and numbers

```
$ cat test.csv | csvhead
    1 Lastname    (Alfalfa)
    2 Firstname   (Aloysius)
    3 SSN         (123-45-6789)
    4 Test1       (40.0)
    5 Test2       (90.0)
    6 Test3       (100.0)
    7 Test4       (83.0)
    8 Final       (49.0)
    9 Grade       (D-)
```

#### Now, only print Lastname and Grade

```
$ cat test.csv | csvfix order -f 1,9
"Lastname","Grade"
"Alfalfa","D-"
"Alfred","D+"
"Gerty","C"
"Android","B-"
"Bumpkin","A-"
"Rubble","C-"
"Noshow","F"
"Buff","B+"
```

#### See how many unique last names there are

```
$ cat test.csv | csvfix order -f 1 | sort | uniq | wc -l
      17
```

There's so many more features! Have fun 🙌🌈

Hit me up [@timcheadle](https://twitter.com/timcheadle) if you have questions.
