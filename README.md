# Created an Ansible playbook which will dynamically load the Variable file named same as OS_Name and just by using the Variable Names .We can configure our target node.

I could have easily solved this used case by using when keyword but to understand ,How more We can easily trick things in playbook and to solve any used cases is always a good thing .

Here I took help of ansible facts and a little manipulation in the playbook

What We want :-

My used case was to build a dynamic playbook which would automatically fetch the OS name and its Version and would work as the name of variable Yaml file .Here I only created a Yaml file of name RedHat and Ubuntu and version of OS 8 and 20 respectively because for demonstration to this practical am using RHEL-8 and Ubuntu-20, In both the file I created multiple variables for package ,Document root path and name of the service of that specific OS supports .Later it would fetch all the details from that specific OS Yaml file to my main playbook .In my playbook ,I instructed to install and start the service of Apache web server .

Which all OS I used for this practical .

I used RHEL 8 (192.168.43.76) , Ubuntu (192.168.43.158).

Here is my Inventory file

![1](https://user-images.githubusercontent.com/67523396/113824742-c1157280-979d-11eb-87e8-49b2c7df3f1f.jpeg)



The following steps to be done ..

STEP 1

I created two Variable_seprated Yaml file with Name and Version of two of the OS I used

Redhat-8.yml

In Redhat-8.yml file ,I defined three variable

package_name: httpd

document_root: /var/www/html/index.html

service_name: httpd


![2](https://user-images.githubusercontent.com/67523396/113824750-c4a8f980-979d-11eb-977f-21a5f2766bc8.jpeg)





Ubuntu-20.yml

In Ubuntu-20.yml file ,I defined three variable

package_name: apache2

document_root: /var/www/html/index.html

service_name: apache2


![3](https://user-images.githubusercontent.com/67523396/113824759-c8d51700-979d-11eb-94ce-b6cb7d511152.jpeg)




STEP 2

I created a Playbook named package.yml .In that playbook I used vars_files module .

![4](https://user-images.githubusercontent.com/67523396/113824783-cf638e80-979d-11eb-9b6a-0031ebb9c833.jpeg)



Instead of giving any file name hardcoded ,here I used ansible_facts and fetch the OS name and Version ,Normally after the output comes out .It would automatically find the variable according to which OS facts belong and configure as we created the variable file.

Here I used vars function as I want that my playbook would dynamically find out which OS it is and in that OS what webpage I want to deploy.


![5](https://user-images.githubusercontent.com/67523396/113824793-d2f71580-979d-11eb-88b3-561f677c0e58.jpeg)





STEP 3

I used package module and in name attribute I used package_name variable which I defined in all of my variable_file .To fetch package_name value I used jinja .


![6](https://user-images.githubusercontent.com/67523396/113824803-d68a9c80-979d-11eb-864e-a571702b7386.jpeg)





STEP 4

I used template module and in dest attribute I used document_root variable which I defined in all variable_file .To fetch document_root value I used jinja .



![7](https://user-images.githubusercontent.com/67523396/113824815-d9858d00-979d-11eb-87c0-6fc72b032c32.jpeg)




In Webpage folder , I created name of Web page same as OS name .They would belong.



![8](https://user-images.githubusercontent.com/67523396/113824824-dc807d80-979d-11eb-881a-fc18bbb14769.jpeg)






STEP 5

I used service module and in name attribute I used service_name variable which I defined in all variable_file .To fetch service_name value I used jinja .



![9](https://user-images.githubusercontent.com/67523396/113824843-e0140480-979d-11eb-8479-f96ff48a9e95.jpeg)





STEP 6

Here I used debug module to show the variable value to get a better understanding .


![10](https://user-images.githubusercontent.com/67523396/113824859-e3a78b80-979d-11eb-8528-b4e82afda902.jpeg)





After running the playbook


![11](https://user-images.githubusercontent.com/67523396/113824872-e73b1280-979d-11eb-928d-b5d78f7a33da.jpeg)



Here, We can confirm that Webserver is successfully configured and hosted.




![12](https://user-images.githubusercontent.com/67523396/113824886-ebffc680-979d-11eb-859c-54758ec8015f.jpeg)









![13](https://user-images.githubusercontent.com/67523396/113824891-eefab700-979d-11eb-8e7c-5f8ae6799e2e.jpeg)






Open for any queries and suggestions .

Thankyou
