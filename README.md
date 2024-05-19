# 📚 Documentation

### Give R/W & exc permission to any file

    sudo chmod 755 <file_name>

### Folder Permission in htdocs file

    cd opt/lampp/htdocs
    sudo mkdir <folder_name>
    sudo chown -R $USER:$USER <folder_name>
    cd <folder_name>
    code .

# Git Setting

### Check git installed or not

    git --version

### initialize git

    sudo apt install git

### 🔧 Configure git

    git config --global user.name <your-name>
    git config --global user.email <your-email>

### Show the global configuration

    git config --list

### Create ssh key for GitHub & system connection or check the 🔗

    Open GitHub setting
    SSH and GPS keys option
    generating SSH keys (click the 🔗 )
    Generation a new SSH key and adding it to the ss-agent(copy the command associated with email)
    open main terminal →paste copied command along with your email [Example : ssh-keygen -t ed25519 -C "sourav@gmail.com"]
    identify directory to save the key file
    enter passphrase(password)
    go to saved file directory
    open .ssh folder -> open .pub file -> copy the text
    paste the key to ssh key of GitHub → enter GitHub password → done.

### Add SSH key 🔗

    https://www.youtube.com/watch?v=jfi9n4y-WFo&t=205s

### SSH 🔑 set or not set checked-out

    ls -al  ~/.ssh

### clone a git repository

For cloning a git repositoty need to copy the ssh/https 🔗 for the repositoty.

    git@github.com:xcompany/x-Managment.git [ssh]
    https://github.com/xcompany/x-Managment.git.git [https]

After copy that 🔗, go to the os terminal create a directory or directly clone the 🔗.

    :git clone <git@github.com:xcompany/x.git>

Then go to the directory

    : cd x-Managment
    : code .

# Git Command

### Stages changes in the all files for the next commit.

    git add .

### Check status of your working directory, showing changes that are staged or unstaged.

    git status

### Records the staged changes as a new commit along with a descriptive message.

    git commit -m "<message>" (-m means message)

### Uploads local commits to a remote repository.

    git push -u origin <branch name>

### Create a new branch & switch to the branch.

    git checkout -b <branch name>

### To check the current branch you are on in a Git repository using the command line.

    git branch

Then git will display a list of all the branches in your repository. The currently checked-out branch will be highlighted with an asterisk (\*).
For example, if you see output like this:

    main
    *feature-branch

It means that you are currently on the "feature-branch" because it has the asterisk next to it.

### Only want to see the current branch.

    git rev-parse --abbrev-ref HEAD

### To switch to a different branch in a Git repository using the command line.

    git checkout <branch-name>

### Fetches changes from a remote repository and merges them into the current branch.

    git pull origin <branch name>

### Rename branch name.

    git branch -m <old branch name> <new branch name>

### Delete a branch.

At first switch to other branch(not delete branch) then delete the branch you want to delete.

    git branch -d <branch-name>

### Delete the .git Directory:

If you want to remove Git version control from a project, you essentially need to delete the hidden .git directory in the root of your project. This will remove all Git-related history, configuration, and tracking from the project.

    rm -rf .git

### Remove an existed git repositoy & add a new repository to the project

    git remote remove origin

    git remote add origin <origin_name>  or
    git remote set-url origin <origin_name>

check the origin

    git remote -v
    git branch
    git push -u origin <branch_name>  or
    git push -f origin <brach_name>

### To clear the cache and update the ignored files :

syntex :

    git rm --cached <file name>

example :

    git rm --cached .env
    git rm --cached serviceAccountKey.json
    git rm -r --cached __pycache__

    git commit -m "Update .gitignore to exclude serviceAccountKey.json"

    git push -u origin <branch name>

# 🐳 Docker

Docker is a software platform that simplifies the process of building, running, managing & distributing application.

### 🐳 Docker installation 🔗

    https://www.youtube.com/watch?v=Z6SLxKZicQc

For command below 🔗

    https://docs.docker.com/desktop/install/ubuntu/

source 2 :

    https://www.youtube.com/watch?v=5_EA3rBCXmU&t=197s

cmd :

    sudo apt-get update
    cd Downloads // go to the docker desktop download folder
    ls
    sudo apt-get install ./<name_of_the_package> //<name_of_the_package> = docker-desktop-4.28.0-amd64.deb
    systemctl --user start docker-desktop

### 🐳 Docker course 🔗

Source 1 :

    https://www.youtube.com/playlist?list=PL8p2I9GklV47v6WZTjHAqdsHxpTIpjRwn

Source 2 :

    https://www.youtube.com/watch?v=31k6AtW-b3Y
    https://www.youtube.com/watch?v=xPT8mXa-sJg

### step : 1 Component of Dockerfile

file name - dockerfile

    FROM node:latest                // which language
    RUN npm install -g nodemon      //install nodemon for instant change
    WORKDIR /app                    // storing directory
    COPY . .                        // source & destination
    RUN npm install                 // install all dependencies
    EXPOSE 8000                     // running port of app
    CMD [ "nodemon", "index.js" ]   // running command

### step : 2 Docker ignore file

file name - .dockerignore

    node_modules
    *.txt

If we want to ignore all files that has '.txt' extention then simply use above method, this will work for all extention

### step : 3 Create an image for an app in docker

After complete the above steps.Suppose my app name is dockertest & i used "image_name" also as dockertest.You can choose your "image_name".

Syntax :

    docker build -t <image_name> <image folder>

Example :

    docker build -t dockertest-image .

Here "." means current folder

![Screenshot from 2024-03-30 14-56-48](https://github.com/s0urav6529/softcopy-note/assets/96060029/915d7254-2e37-43fc-ba3c-8f2d563e7389)

### step : 4 Crate a container using above image name

Syntax :

    docker run -it <image_name>

Example :

    docker run -it dockertest-image

if "image_name" not found in the docker then it will pull the image from the "hub.docker.com" if "image name" existed in "hub.docker"

### step : 5 Port mapping

If want to run this container in your local server. Need to mapping the port

    docker run -it -p 8001:8001 dockertest-image

you can marge the step 4 & 5 like step 5

![Screenshot from 2024-03-30 14-58-48](https://github.com/s0urav6529/softcopy-note/assets/96060029/63d79be8-05c2-476a-a13c-3728be6045cd)

### step : 6 Go to the root of container & do other staffs

    docker exec -it <container_id> bash

![Screenshot from 2024-03-30 15-01-07](https://github.com/s0urav6529/softcopy-note/assets/96060029/274d69eb-e9d6-4393-8aab-5daad8e88b8a)

### Pass the environment variable

Suppose in my code my port is 8000, but further i want that my port must be 4000, due to some reason. So, i can pass the environment variable.

![Screenshot from 2024-03-30 15-03-43](https://github.com/s0urav6529/softcopy-note/assets/96060029/a42f358d-30ef-49d0-9493-232ecf2fcb44)

### Push in hub.docker

If want to push my code in docker hub. Then need to create a repository in the hub.docker & copy the "image_name" from the repositoty.
Copy the "image_name" and create a build locally.

step : 1

![Screenshot from 2024-03-30 15-17-06](https://github.com/s0urav6529/softcopy-note/assets/96060029/b232dd48-c1ba-4d7a-ab3b-2b34872b3221)

step 2 :

![Screenshot from 2024-03-30 15-17-48](https://github.com/s0urav6529/softcopy-note/assets/96060029/5569a128-a26d-409c-ae2c-4f04f739a22b)

step 3 :

![Screenshot from 2024-03-30 15-19-45](https://github.com/s0urav6529/softcopy-note/assets/96060029/e9dae6db-fb48-47d4-a67a-2eb18d2b2c3d)

If not login in hub.docker in locally, then need to login & run this command again

![Screenshot from 2024-03-30 15-23-01](https://github.com/s0urav6529/softcopy-note/assets/96060029/0427ca5c-94ff-4b7c-a407-905264420e0d)

### Run image directly using cmd

    docker run dockertest

### Delete images & containers

For display all images

    docker images
    docker image ls

Normally delete an image

    docker image rm <image name>

For force-fully delete a image, if that image already in use by any container

    docker image rm <image name> -f

For display all containers

    docker ps -a

Normally delete an container

    docker container rm <container name>

For force-fully delete a container, if that container is on running

    docker container rm <container name> -f

### Delete all images & container at a time

    docker system prune -a

### Create image using version

Syntax :

    docker build -t <image name>:<version> <image folder>

Here, 'image name' like dockertest-image, 'version' v1,v2 etc & 'image folder' like '.'

Example :

    docker build -t dockertest-image:v2 .

### Run image container version in cmd

Syntax :

    docker run --name <conatainer name>-<version> -p <port1>:<port2> <image name>:<version>

Here, 'container name' like dockertest-container, 'version' like v1,v2 etc, 'port1' 5001, 'port2' as your docker port & 'image name' like dockertest-image

Example :

    docker run --name dockertest-container-v2 -p 5501:8000 dockertest-image:v2

### Run image container volumn in cmd

    docker run --name dockertest-container-v2 -p 5501:8000 --rm -v /home/sourav/dockertest:/app dockertest-image:v2

Here --rm remove the current container and create a new container, -v is volumn & '/home/sourav/dockertest' is the root path of 'index.js' file & '/app' is the working directory.

### Compose File in Docker

file name - compose.yaml

    services:
        img:
            build: .
            container_name: dockertest-container
            ports:
            - 5501:8000

### Run below command for create a continer

    docker compose up

### Share image on docker hub

Docker hub is a repository of docker images. Where many public images are available.

# Ubuntu installation 🔗

    https://www.youtube.com/watch?v=y7rK4Nd88L4&t=532s

### install(if not) prettier from extensions

create [.vscode] folder→create [settings.json]file and paste below code

    {
        "editor.formatOnSave": true,
        "[javascript]": {
            "editor.formatOnSave": true,
            "editor.defaultFormatter": "esbenp.prettier-vscode"
        }
    }

# ALL types of CDN 🔗

    https://cdnjs.com/libraries

Use this cdn in every header file of ejs.

    Example → <script src="cdn link"></script>

# express-async-handler

It's designed to simplify error handling when dealing with asynchronous routes and middleware functions. It helps to mitigate this by catching any asynchronous errors that might occur within route handlers and forwarding them to the Express error-handling middleware.

    const express = require('express');
    const app = express();
    app.get('/some-route', asyncHandler(async (req, res) => {
    const result = await someAsyncOperation();
    res.json(result);	 // Sending a response
    }));
    // Express error-handling middleware
    app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send('Something went wrong!');
    });

# nodemailer

At first need to intall nodemailer then go to this below 🔗

    https://ethereal.email/

Then go to Create Ethernal Account option.

Copy the nodemailer configuration. Set the user & pass to the .env file of you project.

    const sendResetPasswordMail = async(name,mail,token)=>{

        try {

            //create a SMTP transporter object

            const transporter = nodemailer.createTransport({
                host: 'smtp.ethereal.email',
                port: 587,
                auth: {
                    user: process.env.NODE_EMAIL,
                    pass: process.env.NODE_EMAIL_PASS,
                }
            });

            const mailOptions = {
                from: process.env.NODE_EMAIL,
                to:mail,
                subject: "Reset Password",
                html : "<p>Hi " +
                    name +
                    ', Please click here to <a href = "http://localhost:8000/admin/resetPassword?token=' +
                    token +
                    '"> reset</a> your password.</p>',
            };

            transporter.sendMail(mailOptions,(error,info) =>{
                if(error){
                    console.log(error);
                }else{
                    console.log("Email has been sent:- ",info.response);
                }
            });
        } catch (error) {
            console.log(error.message);
        }
    }

Here,

    <http://localhost:8000/admin/resetPassword>

custom as your need. Then you will get the token from this 🔗 for further use.

# Multer (For upload single & multiple file of any type in local storage) :

Suppose i have a route for upload file of any type and where 'fileUploader' is a middleware to upload file

    xRoute.route("/add")post(isXlogin,fileUploader,addX);

Below the code of 'fileUploader'

    //require a function for upload the file
    const {uploader} = require("../utilities/functions");

    //for upload file
    const fileUploader = function(req,res,next){

        const uploadFile = uploader("product",["image/jpeg","image/jpg","image/png"],
                                10000000,3,"Only .jpg, .jpeg or .png format allowed!");

        // call the upload middleware
        uploadFile.any()(req,res,(err) => {

            if(err){
                return res.status(400).json(err.message);
            }
            else{
                next();
            }
        });
    }

    //exports
    module.exports = {  fileUploader }

Here, the arguments of 'uploader' are sub-folder path to store the file, allowedType,maxFileSize in bytes, maximum number of file to upload at a time, & error message if file type is not matched.

Below the 'uploader' function code

    const uploader = function (subFolderPath, allowedFileType, maxFileSize, maxCount, errorMsg){

        //File upload folder
        const mainDirectory =path.resolve (__dirname,"..");
        const uploadFolder = `${mainDirectory}/public/${subFolderPath}/`;

        //define the storage
        const storage = multer.diskStorage({

            //define destination
            destination : (req,file,cb)=>{
                cb(null,uploadFolder);
            },

            //define fileName
            filename:(req,file,cb)=>{

                //extract file extention
                const fileExtention = path.extname(file.originalname);

                //make a unique file name
                const fileName = file.originalname.replace(fileExtention,"").split(" ").join("-")+ "-" + Date.now() + fileExtention;

                cb(null,fileName);
            },
        });


        const upload = multer({
            storage: storage,
            limits: {
            fileSize: maxFileSize,
            files : maxCount
            },
            fileFilter: (req, file, cb) => {
            if (allowedFileType.includes(file.mimetype)) {
                cb(null, true);
            } else {
                cb(errorMsg);
            }
            },
        });

        return upload;

    }

    //exports
    module.exports = { uploader }

## Add/Update multiple or single file name in database document

    const images = imagesArray(req.files);

    const newX = new xModel({
        ...
        xImage:images,
        ...
    });
    await newX.save();

### Here, the code of 'imagesArray' function

    const imagesArray = function(allfiles){

        let images = [];

        if(allfiles.length > 0){

            for(let i = 0 ;i <allfiles.length ; i++){

                images.push(allfiles[i].filename);

            }
        }else{
            images.push("Image not found");
        }
        return images;
    }

## Delete multiple or single file from local storage folder and document from database

    const xData = await xModel.findOne({_id : req.query.id});

    if(xData){

        // at first remove images from the local storage folder
        const imagesDelete =  unlinkFileFromLocal(xData.xImage,"<sub-filderName>");

        //after remove images we can delete details from database
        const deleteDetails = xModel.findByIdAndDelete({ _id : req.query.id });

        await Promise.all([imagesDelete,deleteDetails]);

        res.status(200).json({ message: "Product deleted successfully !"});
    }

### or from directly 'req.files'

    const images =  imagesArray(req.files);
    await unlinkFileFromLocal(images,"<sub-filderName>");

### Below the 'unlinkFileFromLocal' code

    const unlinkFileFromLocal = async (allFiles,subFolder)=>{

        if(allFiles[0] !== "Image not found"){

            const promises = allFiles.map((fileName) => {

                unlinkFile(fileName,subFolder)
                .then(res=>{
                    console.log("File deleted successfully !");
                })
                .catch(error=>{
                    console.log(error);
                });
            });

            return await Promise.all(promises);
        }
        return;
    }

### Below the 'unlinkFile' code

    const unlinkFile = async(fileName,subFolderPath) => {

        try {

            const mainDirectory =path.resolve (__dirname,"..");
            const folderPath = `${mainDirectory}/public/${subFolderPath}/`;

            const filePath = path.join(folderPath,fileName);

            const fileAccess = fs.access(filePath, fs.constants.F_OK);
            const fileUnlink = fs.unlink(filePath);

            retrun await Promise.all([fileAccess,fileUnlink]);

        } catch (error) {
            return error;
        }
    }

# Category/subcategory wise product delete

    const deleteSubCategory = async(req, res) => {

        try {

            //find product details of that sub-category
            const productsDetails = await productModel.find({subCategoryId : req.query.id});

            //delete each product image from the local folder
            productsDetails.forEach(async(details) => {

                await unlinkFileFromLocal(details.productImage,"product");

            });

            const deleteSubCategory = subCategoryModel.findByIdAndDelete({_id:req.query.id});

            const deleteProducts = productModel.deleteMany({subCategoryId:req.query.id});

            await Promise.all([deleteSubCategory,deleteProducts]);

            res.status(200).json({message:"Sub-category deleted successfully !"});

        } catch (error) {
            res.status(400).json({error,message:"Problem during delete sub-category !"});
        }
    }

# Cors

Cross-Origin Resource Sharing (CORS) is a security feature implemented by web browsers that restricts webpages from making requests to a different domain than the one that served the original web page.

    npm install cors

Now in index.js

    const express = require('express');
    const cors = require('cors');

    const app = express();

    // Enable CORS for all routes

    const corsOptions = {
        origin: 'http://localhost:8080',                // Specify the allowed origin (or use a function for dynamic origins)
        methods: 'GET,HEAD,PUT,PATCH,POST,DELETE',      // Specify the allowed HTTP methods
        allowedHeaders: 'Content-Type,Authorization',   // Specify the allowed headers
        credentials: true,                              // Allow credentials (like cookies) to be sent with the request
        optionsSuccessStatus: 204,                      // Specify the HTTP status code for successful preflight requests
        preflightContinue: false,                       // Disable preflight requests caching
        maxAge: 3600,                                   // Specify the maximum time (in seconds) that a preflight request can be cached
    };

or an array of allowed origins, can also use a function to dynamically determine the allowed origins based on the request.

    const corsOptions = {
        origin: function (origin, callback) {
            // Check if the origin is allowed
            const allowedOrigins = ['http://localhost:8080', 'https://yourclientdomain.com'];
            if (!origin || allowedOrigins.includes(origin)) {
                callback(null, true);
            } else {
                callback(new Error('Not allowed by CORS'));
            }
        },
        // other options...
    };

    app.use(cors(corsOptions));

    // Your routes and other middleware go here
    const port = 3000;
    app.listen(port, () => {
        console.log(`Server is running on port ${port}`);
    });

# 🐍 installation command for ubunto

    sudo apt update
    sudo apt install software-properties-common
    sudo add-apt-repository ppa:deadsnakes/ppa
    sudo apt update
    sudo apt install python3.12
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.12 2
    sudo apt install python3.12-dev python3.12-venv python3.12-distutils python3.12-gdbm python3.12-tk python3.12-lib2to3

Now to see the version

    python --version

### face_recognition pakage

    sudo apt-get install build-essential cmake
    sudo apt-get install libopenblas-dev liblapack-dev
    sudo apt-get install libx11-dev libgtk-3-dev
    sudo apt-get install libboost-all-dev
    pip install face_recognition

### cv2 pakage

    pip install opencv-python

### .env file

![Screenshot from 2024-02-22 11-03-14](https://github.com/s0urav6529/softcopy-note/assets/96060029/21b8392e-5073-4790-9969-2936040ec633)

    pip install python-dotenv python-decouple

![Screenshot from 2024-02-22 11-03-30](https://github.com/s0urav6529/softcopy-note/assets/96060029/2f626fb8-2deb-484b-b20b-f339b9415a2e)

# installation of XAMPP

    https://www.apachefriends.org/

Now, go to the directory where this file is downloaded using terminal,then copy & peste those command

    sudo chmod 755 xampp-linux-x64-8.2.12-0-installer.run
    sudo ./xampp-linux-x64-8.2.12-0-installer.run

After successful installation, go main terminal

    cd /opt/lampp/              [xammp installation path]
    ls
    cd htdocs/
    sudo mkdir phpsite
    cd phpsite
    code .

    localhost:80/phpsite [visite the site]

# 🔥 installation

    https://firebase.google.com/docs/cli#cli-ci-systems  [website]

    curl -sL https://firebase.tools | bash
    firebase login
    firebase projects:list

# redis installation step by step

For install using snap...

    sudo snap install redis

For enable redis...

    sudo snap enable redis

For start redis...

    sudo snap start redis

For stop redis...

    sudo snap stop redis

For restart redis...

    sudo snap restart redis

For check the redis status...

    sudo snap services

For connect the redis server using snap

    redis.cli

If want to make redis-cli, go to main terminal

    sudo snap alias redis.cli redis-cli

    sudo snap unalias redis-cli   // for change
