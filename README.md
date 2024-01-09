# Git Setting

### Check git installed or not

    git --version

### initialize git

    sudo apt install git

### Configure git

    git config --global user.name <your-name>
    git config --global user.email <your-email>

### Show the global configuration

    git config --list

### Create ssh key for GitHub & system connection or check the link

    Open GitHub setting
    SSH and GPS keys option
    generating SSH keys (click the link )
    Generation a new SSH key and adding it to the ss-agent(copy the command associated with email)
    open main terminal →paste copied command along with your email [Example : ssh-keygen -t ed25519 -C "sourav@gmail.com"]
    identify directory to save the key file
    enter passphrase(password)
    go to saved file directory
    open .ssh folder -> open .pub file -> copy the text
    paste the key to ssh key of GitHub → enter GitHub password → done.

### Add SSH key link

    https://www.youtube.com/watch?v=jfi9n4y-WFo&t=205s

### SSH key set or not set checked-out

    ls -al  ~/.ssh

## Git Command

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

# Ubuntu installation

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

### For uninstall a package

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

### COOKIE SECRET Link

    https://api.wordpress.org/secret-key/1.1/salt/

take one key & go below link to genarate hash key

    https://emn178.github.io/online-tools/sha1.html

### JWT ACCESS TOKEN SECRET link

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

### ALL types of CDN link

    https://cdnjs.com/libraries

Use this cdn in every header file of ejs.

    Example → <script src="cdn link"></script>

### When we use app.use()

    For use any middleware(error handler, router), body-parser,

### Mongo server:

Starts cmd:

    sudo systemctl start mongod

Status check cmd:

    systemctl status mongod

### http-errors

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

### express-async-handler

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

### body-parser

A "body parser" is a middleware used to parse the body of incoming HTTP requests,this body can include data of the requested method.This data could be in various formats such as JSON, URL-encoded data, or even multipart form data (for file uploads).The purpose of a body parser middleware is to take the raw data from the request and convert it into a more usable format that can be accessed in your route handlers or middleware functions.

Install cmd : npm install body-parser

Import as : const asyncHandler = require(“body-parser”);

Use in main server.js or app.js

    app.use(bodyParser.urlencoded({ extended: true })) ; parse application/x-www-form-urlencoded
    app.use(bodyParser.json()) ; parse application/json

### bcrypt

It return a promise thus we need to use await. Bcrypt.hash() is hashed any password for protection & also compare the given password with hashed password during the login authentication or any occasion.

Password hashing

    const hashedPassword = await bcrypt.hash(password, 10);

Compare password of the user

    if (await bcrypt.compare(password, user.password)) {/...}

### RegExp for search

For searchBox we use RegExp so that search can be dynamic.

#### search Route

        productRoute.route("/searchProduct/:item").get(searchProduct);

        //url -> http://localhost:8000/product/searchProduct/<item>

Make a special charecter escape function in utilities folder and named as escape.

utilities/escape.js

    // function for regular expression
    const escape = function(str){
        return str.replace(/[-\/\\^$*+?.()|[\]{}]/g, "\\$&");
    };

    //exports
    module.exports = escape;

#### Create a controller for this search

        const escape = require("../utilities/escape")

        const searchProduct = async(req, res)=>{

            try {

                //fetch the query string
                const searchQuery = req.params.item;

                const category = new RegExp(escape(searchQuery),"i");
                const subCategory = new RegExp(escape(searchQuery),"i");
                const productName = new RegExp(escape(searchQuery),"i");
                const price = new RegExp("^" + escape(searchQuery),"i");
                const description = new RegExp(escape(searchQuery),"i");

                //now search this expession from the database
                if(searchQuery !== ""){

                    const productData = await productModel.find({
                        $or:[{
                            category:category
                        },{
                            subCategory:subCategory
                        },{
                            productName:productName
                        },{
                            price:price
                        },{
                            description:description
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

### nodemailer

At first need to intall nodemailer then go to this below link

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

custom as your need. Then you will get the token from this link for further use.

## mongoose

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

Suppose i have a route for upload file of any type and where 'avaterUpload' is a middleware to upload file

    xRoute.route("/add")post(isXlogin,avatarUpload,addX);

Below the code of 'avaterUpload'

    //require a function for upload the file
    const {uploader} = require("../utilities/functions");


    function avatarUpload(req,res,next){

        // set all storage & format type
        const upload = uploader("product",["image/jpeg","image/jpg","image/png"],
        10000000,3,"Only .jpg, .jpeg or .png format allowed!");

        // call the upload middleware
        upload.any()(req,res,(err)=>{

            if(err){
                res.status(400).json(err.message);
            }
            else{
                next();
            }
        })
    }

    module.exports = avatarUpload;

Here, the arguments of 'uploader' are sub-folder path to store the file, allowedType,maxFileSize in bytes, maximum number of file to upload at a time, & error message if file type is not matched.

Below the 'uploader' function code

    const uploader = function (subFolderPath, allowedFileType, maxFileSize,maxCount, errorMsg){

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

## Add multiple or single file name in database

    let image = [];

    if(req.files && req.files.length > 0){
        for(let i = 0 ;i <req.files.length ; i++){
            image.push(req.files[i].filename);
        }
    }else{
        image.push("Image not found");
    }

    const newX = new xModel({
        ...
        xImage:image,
        ...
    });
    await newX.save();

## Delete multiple or single file from local storage

    const xData = await xModel.findOne({_id : req.query.id});

    if(xData){

        // at first remove the x image from the local storage
        const allFiles = xData.xImage;

        if(allFiles[0] !== "Image not found"){

            const promises = allFiles.map((fileName)=>{
                unlinkFileFromLocal(fileName,"product");
            });

            await Promise.all(promises);
        }
        await xModel.findByIdAndDelete({ _id : req.query.id });
        res.status(200).json({....});
    }
