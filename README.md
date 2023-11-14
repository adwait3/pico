# pico
this is my repository for writeups of the pico ctf challanges


# PYTHON WRANGLING
## PROBLEM:
Python scripts are invoked kind of like programs in the Terminal... Can you run this Python script using this password to get the flag?
## solution:
in thie problem we were given three files out of which one was a python file ,so first i tried to run it on a web compiler but it led to errors, i then looked at the hints given which were:
* Get the Python script accessible in your shell by entering the following command in the Terminal prompt: $ wget https://mercury.picoctf.net/static/0bf545252b5120845e3b568b9ad0277e/ende.py
* $ man python
These made me realise that this problem must require terminal and not a python compiler, after looking at the man page i tried running the python file through the terminal in shwll using python3. and it gave me an output reguarding the commands usage.

![Screenshot from 2023-11-04 13-11-59](https://github.com/adwait3/pico/assets/148553626/a3683bcf-16c5-462e-8294-6e1d30c4db65)

I followed it and used -d flag (for decode) with our file and then provided the password which gave me the flag.
## FLAG
picoCTF{4p0110_1n_7h3_h0us3_6008014f}


# keygenme-py
## PROBLEM:
we are just given a code with no hints.


## BACKGROUND:
first i tried to run the code on a web compiler but i had trouble because of the cryptography module:
![Screenshot from 2023-11-05 19-38-11](https://github.com/adwait3/pico/assets/148553626/66297520-9fb2-41a7-9170-7b6889a476a5)

after this i tried running the code on vs code but had issues with compiling it which i could not rectify or understand.
SO i tried running the code on idle after installing cryptography module via the terminal.

## SOLUTION:
i was successfully able to run the code on idle after a silpe debugging of the try and except block,which gave me the output as
![Screenshot from 2023-11-05 19-19-25](https://github.com/adwait3/pico/assets/148553626/f6ac6edb-4230-4849-adeb-4c87b19dd3d2)

 after this i tried reading the code and realised the answer only concerns the enter_liscence()
functionand rest were redundant, so i focused my attention there,
![Screenshot from 2023-11-05 19-24-08](https://github.com/adwait3/pico/assets/148553626/1bc4f7ba-47bf-4cdd-8e45-0ce3915fffab)

this block tells us that
* the lenth of the key should be equal to the key_full_template_trial which is the concatenated string of key_part_static1_trial + key_part_dynamic1_trial + 
 key_part_static2_trial , so we can guess the length of the key from here which is picoCTF{1n_7h3_|<3y_of_xxxxxxxx} characters long 
* the first part of string is equal to the static portion.
  ow we have to find the second part instead of the xxxxxx portion, loooking at further code we figure out what the next charaxters should be equal to in order to not break from the loop, so i print the statements with which we are checking the key 
![Screenshot from 2023-11-05 19-30-58](https://github.com/adwait3/pico/assets/148553626/82b1fe59-3ef4-4991-8583-e717815b410f)

  this gives me an error stating that Unicode-objects must be encoded before hashing so i look for what this means and fnd out that we are given another username bUsername_trial which is already encoded so i use it while printing and this given me the output and i build up my key using thiese and sure enough the key is right and im able to access the full verion of the calculator.
  ![Screenshot from 2023-11-05 19-35-50](https://github.com/adwait3/pico/assets/148553626/48585f5e-a6ff-4ca7-9bc7-5aad7ac8a69a)

  ## KEY;
  picoCTF{1n_7h3_|<3y_of_0d208392}

  # STOONKS
  ## problem
  I decided to try something noone else has before. I made a bot to automatically trade stonks for me using AI and machine learning. I wouldn't believe you if you told me it's unsecure! vuln.c nc mercury.picoctf.net 33411
  * hint = Okay, maybe I'd believe you if you find my API key.

## SOLUTION
 first after downloading the code i tried running it on cs code on my machine which gave me an error in the following :
 ![Screenshot from 2023-11-08 10-45-22](https://github.com/adwait3/pico/assets/148553626/2e1d9cef-c3e7-4bda-8fa7-5d00162261c5)
 as the format (data type ) of user_buf was not defined in the code.
 after studying a bit about printf and how it works i got to know that it prints what we want from a stack which is known as the buffer eg in printf ("%s", a)
 %s is our format in which we want the output and a is like an address in the buffer which we want in that particular format, in our code we only have a user_buf and if that is not present in the buffer and format is not defined , the printf statement just starts giving output of whatver is in the stack(buffer), we can specify the format of this output buy using format specifiers , in this problem i wanted all of the stuff whihc is in the stack since we dont know what format we are looking for so we use %x (hex) as the specifier as 
 ![Screenshot from 2023-11-08 11-44-53](https://github.com/adwait3/pico/assets/148553626/2cec20ba-60d0-47ec-a3d2-ef4f9b02717b)

which gives us the output now we convert it into ascii using cyberchef
![Screenshot from 2023-11-08 11-54-21](https://github.com/adwait3/pico/assets/148553626/37cc6f08-cc8d-4142-950d-f9cb2d7fe70c)
in this i was able to find something which looked like my flag but it was jumbled so i truncated the excess hex to just get my flag 
![Screenshot from 2023-11-08 11-55-51](https://github.com/adwait3/pico/assets/148553626/2c16e2a2-e480-42cd-9f9d-e345c14b2f26)
now after reading a bit more abt how stuff is stored ina buffer i found i out that a maximim of 32 bits are stored in every slot of the stack and each ascii value is 8 bits that means 4 characters and that made sence as in the jumbled flag i could figure out that every group of 4 characters was written backwards 
so i manually broke the jumbled flag into parts of 4 and reversed each of them  and conctanated them together which gave me 

## FLAG
picoCTF{I_l05t_4ll_my_m0n3y_a24c14a6}


# CAAS
## problem 
we are given a url of a web service in which we can make a cow say whatever we want and the code for the service in javascript.

## solution
First i opened the the url and from there we are directed as to how can we use the serive to mak the cow say words.
![Screenshot from 2023-11-14 19-12-56](https://github.com/adwait3/pico/assets/148553626/78e12bb6-c4bc-462c-88a9-c03b74288ebb)
i tried saying hi 
after this i look at the js code which is given to us
![Screenshot from 2023-11-14 19-06-52](https://github.com/adwait3/pico/assets/148553626/7ea04c10-348d-4638-9644-e84cbc53b4a2)

and find out that   exec(`/usr/games/cowsay ${req.params.message}`, {timeout: 5000}, (error, stdout) => {
command gives our message input to the command prompt and sends the commands output as a response
and that
app.listen(3000, () => {
  console.log('listening');
});
starts the server and makes it listen on the 3000 port.
this made me realise that i can type commands in the url as https://caas.mars.picoctf.net/cowsay/hi;ls;cat%20falg.txt to run the lines directly in the comand prompt and get the output 
![Screenshot from 2023-11-14 19-07-10](https://github.com/adwait3/pico/assets/148553626/d1c8dec9-963b-4d4e-ae53-9629f66cad6f)

![Screenshot from 2023-11-14 19-09-02](https://github.com/adwait3/pico/assets/148553626/e3bd85b9-9a58-4d7a-a21e-9cc6c7d34a9d)

after reading the flag.txt file we get the flag , we use %20 for space as a url cannot have spaces.

## flag
picoCTF{moooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo0o}



# 
  
