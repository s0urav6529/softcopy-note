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

npm install dotenv[for environment setup] express nodemon body-parser[for parsing object,json & other unreadable file] http-errors[for error-handling] cookie-parser[for cookie] jsonwebtoken[for creating json] express-async-handler[for error handling] mongoose[for database] bcrypt[for hashing] moment[] ejs[for ejs template] express-validator[for validating result] multer[for file upload] socket.io[for real time communication] express-session[for create login session] nodemailer[for sending mail in case of forget password] randomstring[use as a token in case of forget password etc]

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

Replace <database> with your database name

### COOKIE SECRET Link

    https://api.wordpress.org/secret-key/1.1/salt/

take one key & go below link to genarate hash key

    https://emn178.github.io/online-tools/sha1.html

### JWT ACCESS TOKEN SECRET link

    https://www.javainuse.com/jwtgenerator
