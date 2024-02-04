# 📚 Documentation

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

## npm

For install all the dependency after clone a git repository that exist in this repository, the command is below.

    npm i --force

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

# AWS - s3

### s3- View in AWS

![Screenshot from 2024-01-31 11-28-29](https://github.com/s0urav6529/softcopy-note/assets/96060029/f76a3102-d50f-4a80-b491-f6f77147dfae)

### How to access public files form s3

![Screenshot from 2024-01-31 11-35-17](https://github.com/s0urav6529/softcopy-note/assets/96060029/bd397dee-b962-48c1-a673-c9d99e1b6021)

Here, 'piyusgargdev-yt' is the bucket name and 's3.ap-south-1.amazonaws.com' is the service name & rest is the files name or key.

### How to access private files form s3

![Screenshot from 2024-01-31 11-47-39](https://github.com/s0urav6529/softcopy-note/assets/96060029/a5147e9e-384d-44a2-bb7b-0b4dd2fb8137)

This will not work because there is no presigned URL for access, so we need token & singiture to access.

So, need to make an account on s3 & get access token so that private files can be accessed. Suppose we have an user named 'John' & create an access token of this user so whenever this user tries to access files then s3 checkes if this token is valid for access files , if yes then ok otherwise it will denied again.

![Screenshot from 2024-01-31 11-53-13](https://github.com/s0urav6529/softcopy-note/assets/96060029/576555c7-e956-40d5-bf9d-0f04783b78f7)

There are two types of presigned URL (GET & PUT object)

### s3 image upload using multer & multer-s3

Configuration code of s3

    //@external module
    const { S3Client } = require('@aws-sdk/client-s3');
    const multerS3 = require('multer-s3');
    const path = require("path");

    //@configure AWS SDK with your credentials and region
    const awsConfig = {
        region: process.env.AWS_BUCKET_REGION,
        credentials: {
            accessKeyId: process.env.AWS_ACCESS_KEY,
            secretAccessKey: process.env.AWS_SECRET_KEY
        },
    };

    //@create s3 client instance
    const s3Client = new S3Client(awsConfig);

    //@create storage configuration
    const storageConfig = multerS3({

        s3: s3Client,
        bucket: process.env.AWS_BUCKET_NAME,
        acl: 'public-read',
        contentType: multerS3.AUTO_CONTENT_TYPE,

        key: (req, file, cb) => {
            const fileExtention = path.extname(file.originalname);
            const key = file.originalname.replace(fileExtention,"").split(" ").join("-")+ "-" + Date.now() + fileExtention;
            cb(null, key);
        },
    });

    //@exports
    module.exports = { storageConfig };

upload code for any route

    const upload = multer({
        storage : storageConfig
    });

    //for single file upload
    router.route("/").post(upload.single('file'),(req,res) => {

        //uploaded file url
        res.send(req.file.location);
    });

    //for multiple file upload
    router.route("/").post(upload.array('files',3),(req,res) => {

        //uploaded file url
        req.files.map((file)=>{
            console.log('File uploaded to S3:', file.location);
        });
    });

# 🐳 Docker

Docker is a software platform that simplifies the process of building, running, managing & distributing application.

### 🐳 Docker installation 🔗

    https://www.youtube.com/watch?v=Z6SLxKZicQc

For command below 🔗

    https://docs.docker.com/desktop/install/ubuntu/

### 🐳 Docker course 🔗

    https://www.youtube.com/playlist?list=PL8p2I9GklV47v6WZTjHAqdsHxpTIpjRwn

### Component of Dockerfile

file name - dockerfile

    FROM node:latest                // which language
    RUN npm install -g nodemon      //install nodemon for instant change
    WORKDIR /app                    // storing directory
    COPY . .                        // source & destination
    RUN npm install                 // install all dependencies
    EXPOSE 8000                     // running port of app
    CMD [ "nodemon", "index.js" ]   // running command

### Docker ignore file

file name - .dockerignore

    node_modules
    *.txt

If we want to ignore all files that has '.txt' extention then simply use above method, this will work for all extention

### Create image for an app in docker

Suppose my app name is dockertest & i used image name also as dockertest.

Syntax :

    docker build -t <image name> <image folder>

Example :

    docker build -t dockertest-image .

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

# Open a new project on vs-code:

### Open main terminal

    [mkdir appname](exp : contact-app) → [cd appname] → [code .] (Will take you to vs-code)

### Go to vs-code terminal and initialize the project

    npm init →then give the info as instruction

### Installation external module

    npm install dotenv [for environment setup]
    express
    nodemon
    body-parser [for parsing object,json & other unreadable file]
    http-errors [for error-handling]
    cookie-parser [for cookie]
    jsonwebtoken [for creating json]
    express-async-handler [for error handling]
    mongoose [for database]
    bcrypt [for hashing]
    moment [Moment module is used for parsing, validating, manipulating, and displaying dates and times in JavaScript]
    ejs [for ejs template]
    express-validator [for validating result]
    multer [for file upload]
    socket.io [for real time communication]
    express-session [for create login session]
    nodemailer [for sending mail in case of forget password]
    randomstring [use as a token in case of forget password etc]
    socket.io [for install web socket]

### Go to pakage.json and change this script part

    "scripts": {
        "start": "NODE_ENV=development nodemon app.js" or
        "start": "nodemon app.js",
        "prod": "NODE_ENV=production node app.js",
        "test": "mocha test/integration/fileRoutes.test.js",
    },

### For uninstall a package 📦

    npm uninstall package-name

### install(if not) prettier from extensions

create [.vscode] folder→create [settings.json]file and paste below code

    {
        "editor.formatOnSave": true,
        "[javascript]": {
            "editor.formatOnSave": true,
            "editor.defaultFormatter": "esbenp.prettier-vscode"
        }
    }

### For run project

    npm start

### Create .env file paste this code (To access this file data use process.env.PORT/APP...etc)

    PORT=5000
    APP_NAME=
    MONGO_CONNECTION_STRING=mongodb://localhost/<databasename>
    MONGOURI=mongodb+srv://Foodline:<password>@cluster0.szpnieh.mongodb.net/<databasename>?retryWrites=true&w=majority [for mongo atlas]
    COOKIE_SECRET=from the below (Cookie secret link)
    JWT_ACCESS_TOKEN_SECRET=from the below (jwt link)
    JWT_EXPIRY=86400000  // as your choice in milisecond
    COOKIE_NAME= anything
    APP_URL=http://localhost:portno

Replace <database> with your database name

### 🍪 COOKIE SECRET 🔗

    https://api.wordpress.org/secret-key/1.1/salt/

take one key from the above 🔗 & go below 🔗 to genarate hash key

    https://emn178.github.io/online-tools/sha1.html

### JWT ACCESS TOKEN SECRET 🔗

    https://www.javainuse.com/jwtgenerator

### Import different-types of external module in app.js/index.js (entry file)

    const express = require("express");
    const dotenv = require("dotenv").config();
    const http = require("http");
    const asyncHandler = require(“express-async-handler”);     [use in desired  file]

    const app = express();

    const server = http.createServer(app);
    server.listen(process.env.PORT, () => {
    console.log(`Listening to port ${process.env.PORT}`);
    });

### For Rest API install Thunder Client or Post Man from (extensions vs-code) or postman in outside

    For GET, POST, PUT, DELETE send request

# ALL types of CDN 🔗

    https://cdnjs.com/libraries

Use this cdn in every header file of ejs.

    Example → <script src="cdn link"></script>

### When we use app.use()

    For use any middleware(error handler, router), body-parser,

# Mongo server:

Starts cmd:

    sudo systemctl start mongod

Status check cmd:

    systemctl status mongod

# http-errors

For create error it provides a function called createError(“type the error”);

Some error code

    • 400    BadRequest
    • 401    Unauthorized
    • 402    PaymentRequired
    • 403    Forbidden
    • 404    NotFound
    • 500    InternalServerError
    • 502    BadGateway
    • 504    GatewayTimeout

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

# body-parser

A "body parser" is a middleware used to parse the body of incoming HTTP requests,this body can include data of the requested method.This data could be in various formats such as JSON, URL-encoded data, or even multipart form data (for file uploads).The purpose of a body parser middleware is to take the raw data from the request and convert it into a more usable format that can be accessed in your route handlers or middleware functions.

Install cmd : npm install body-parser

Import as : const asyncHandler = require(“body-parser”);

Use in main server.js or app.js

    app.use(bodyParser.urlencoded({ extended: true })) ; parse application/x-www-form-urlencoded
    app.use(bodyParser.json()) ; parse application/json

# bcrypt

It return a promise thus we need to use await. Bcrypt.hash() is hashed any password for protection & also compare the given password with hashed password during the login authentication or any occasion.

Password hashing

    const hashedPassword = await bcrypt.hash(password, 10);

Compare input password of the user with the hashed password of the database

    if (await bcrypt.compare(password, user.password)) {/...}

Here 'password' is input password & 'user.password' is hashed password

# RegExp for search

For searchBox we use RegExp so that search can be dynamic.

#### search Route

        productRoute.route("/searchProduct/:item").get(searchProduct);

        //url -> http://localhost:8000/product/searchProduct/<item>

Make a special charecter escape function in utilities folder and named as escape.

utilities/functions.js

    // function for regular expression
    const escapeString = function(str){
        return str.replace(/[-\/\\^$*+?.()|[\]{}]/g, "\\$&");
    };

    //exports
    module.exports = {escapeString};

#### Create a controller for this search

        const {escapeString} = require("../utilities/functions.js")

        const searchProduct = async(req, res)=>{

            try {

                const searchQuery = new RegExp(escapeString(req.params.item),"i");
                const price = new RegExp("^" + escape(req.params.item),"i");

                //now search this expession from the database
                if(req.params.item !== ""){

                    const productData = await productModel.find({
                        $or:[{
                            category: searchQuery
                        },{
                            subCategory: searchQuery
                        },{
                            productName: searchQuery
                        },{
                            price: price
                        },{
                            description: searchQuery
                        }]
                    });

                    if(productData.length > 0){
                        res.status(200).json({message:"Product found",productData});
                    }
                    else{
                        res.status(200).json({message:"No product found!"});
                    }
                }
            } catch (error) {
                res.status(400).json({error,message:"Errors occurs during search product"});
            }
        }

^: Asserts the start of the string.

$: Asserts the end of the string.

"i": Specifies a case-insensitive match.

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

# mongoose

### populate

    const searchAllProduct = async(req,res) => {

        try {

            //just load all data from the database
            const allData = await productModel.find({}).select('productName').
                            populate({path:'categoryId subCategoryId' , select:'category subCategory'});

            if(allData.length > 0){
                res.status(200).json({allData,message:"All data loaded successfully !"});
            }
            else{
                res.status(200).json({message:"No data found !"});
            }

        } catch (error) {
            res.status(400).json({error,message:"Errors occur during search all products !"});
        }
    }

### Create a virtual 'id' instead of '\_id'

Suppose we have a Schema name 'userSchema'.

    userSchema.virtual('id').get(function(){
        return this._id.toHexString();
    });
    userSchema.set('toJSON',{
        virtuals:true,
    });

### findByIdAndUpdate() Function

The findByIdAndUpdate() function is used to find a matching document, updates it according to the update arg, passing any options, and returns the found document (if any) to the callback.

    const updateDocument = async (id) => {
        try {
            const updatedResult = await User.findByIdAndUpdate(
                { _id: id },
                {
                    profession: "Backend Developer",
                },
                {
                    new : true
                }
            );
            console.log(updatedResult);
        } catch (error) {
            console.log(error);
        }
    };

### findOneAndUpdate() Function

    const subCategoryData = await subCategoryModel.findOneAndUpdate(
        { categoryId : req.params.id },
        { category : categoryData.category},
        { new:true}
    );

### updateMany() Function

    await subCategoryModel.updateMany(
        { categoryId : req.params.id },
        { category : categoryData.category},
        { new:true}
    );

### For delete any object from the array. You should use the 'update' method with the '$pull' operator to remove the specific element from the array.

    const result = await Order.updateOne(
        { 'orderDetails.orderId': orderId },
        { $pull: { 'orderDetails': { 'orderId': orderId } } }
    );

    if (result.matchedCount > 0) {
        //successful deletation
    } else {
        //error
    }

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

# Format Date

Suppose, 'sDate' is a const variable need to change the format.

    const startDate = formatDate(sDate);

formateDate funtion is below.

    const moment = require("moment");

    const formatDate = function(date){

        const parseDate = moment(date,'DD-MM-YYYY',true);

        if(parseDate.isValid()){
            return parseDate.format('YYYY-MM-DD');
        }
        else {
            console.log("Invalid date format !");
            return;
        }
    }
