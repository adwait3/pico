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

