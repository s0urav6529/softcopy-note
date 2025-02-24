# 📚 Documentation

### Give R/W & exc permission to any file

    sudo chmod 755 <file_name>

### Folder Permission in htdocs file

    cd opt/lampp/htdocs
    sudo mkdir <folder_name>
    sudo chown -R $USER:$USER <folder_name>
    cd <folder_name>
    code .

### Install composer

At first check php installed or not

    php --version

Then, execute those 5 commands

    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
    php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
    php composer-setup.php
    php -r "unlink('composer-setup.php');"
    sudo mv composer.phar /usr/local/bin/composer

Now, check installed successfully or not by below commnad

    composer

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

## Linux server Configuration:

### Installing PHP 8.2/8.3+ on ubuntu 23.04+ server

    sudo add-apt-repository --remove ppa:ondrej/php

then,

    sudo apt update

You will need to edit your repository source file as follows:

    sudo nano /etc/apt/sources.list

and enter

    deb https://ppa.launchpadcontent.net/ondrej/php/ubuntu jammy main

then run

    sudo apt update

after which you should now be able to install your php version using 8.2 as an example

    sudo apt install php8.3

For more details check-out below link

    https://dev.to/niyiojeyinka/installing-php-8283-on-ubuntu-2304-4op3

### Install Mysql:

    sudo apt update

    sudo apt install mysql-server

    sudo systemctl start mysql

    sudo systemctl status mysql

##### create a user for mysql:

    CREATE USER 'new_username'@'localhost' IDENTIFIED BY 'new_password';

    GRANT ALL PRIVILEGES ON *.* TO 'new_username'@'localhost';

    FLUSH PRIVILEGES;

    EXIT;

### Install phpmyadmin:

    sudo apt update

    sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl

    sudo phpenmod mbstring

    sudo systemctl restart apache2

##### For config phpadmin in with server:

    sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-enabled/phpmyadmin.conf

    sudo systemctl restart apache2

Access the phpmyadmin using...

    http://your_server_ip/phpmyadmin

##### Remove a directory from server

    sudo rm -r folder_name

or

    sudo rm folder_name

##### Create a configure site file

    sudo nano /etc/apache2/sites-available/project.conf

then edit here & save the file

### How to upload a php project in apache server

    https://codewithsusan.com/notes/deploy-laravel-on-apache

### Add ssh key for a server

    https://codewithsusan.com/notes/ssh-keys-and-github
