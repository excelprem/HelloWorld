///// Common variables /////
env.git_repo_name="git@github.com/excelprem/HelloWorld" // update this value as created in Step 9 above
env.git_id="a4e1edab-6a97-4c62-8404-e298a616a575"  // update this value as created in Step 9 above

node("master")
{

// STAGE is a labeled block.
//Develop success 
stage 'CI Build'

//##########################################################
// SCM is a special variable which instructs the CHECKOUT step to clone the specific revision which triggered this Pipeline
//##########################################################
checkout scm

// Below code will run the Build steps for a given application
sh '''
echo " This is a CI build Step"
###### Specify your application specific Build Steps Below ####################
###### For instance refer below build steps for node.js Application #######
# npm install
# npm run webpack
####################################################################

'''

// STAGE is a labeled block.
stage 'Merge Build'

// Below code will TAG the current state of code so that later it can be merged to Master branch

sh '''
echo " This is a Merge Build Step"

# Adding Tag
git tag -a ${BUILD_TAG} -m 'CI commit tag';

# Remove the HTTP origin
git remote rm origin;

# Add the SSH origin for your repository
git remote add origin "${git_repo_name}";

# Push the tag
git push origin ${BUILD_TAG};
'''

// Below code will checkout the Master branach of a given Repository &amp; then Merge the Pull Request Tag to Master
git credentialsId: "${env.git_id}", url: "${env.git_repo_name}"

sh '''

git fetch --tags;

# Merge the Pull Request Tag
git merge ${BUILD_TAG};

#Push the code
git push origin master
'''
}
