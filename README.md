# create-svelte

Hellooooo most of the things here is written by [`create-svelte`](https://github.com/sveltejs/kit/tree/master/packages/create-svelte). Thx svelte for saving me the time to write a README.md file

## Developing

So first, you'll want to install dependencies with `npm install`. After that, we can start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.

## How to add pages

In +layout.svelte that correspond to the navbar on homepage, there's a class called AppPages to represent the different pages. To create an instance, pass in the Page Title and path to folder as arguments. ie "new AppPages("Invoice Upload", "/invoice_upload").

After creating the instance, push that instance into the list called appPagesList. The existing code is designed to push items in appPagesList to generate the links in navbar.

## Routing in the app

FE will try and keep this updated everytime we make a change. Ideally, it should show how the pages/components are currently implemented

Page
* dashboard is just empty dashboard. No links because navbar is right above.
* under invoice_upload, the submit button will render child component "resultComponent" to show the return of ocr API, and for them to edit missing values if needed.
* under invoice_search, there are 4 types of child components that correspond to changes in the url:
    1. by default it will render CompanySearchComponent
        * to choose the company under your name
    2. entering /invoice_search/company1 will render InvoiceSearchComponent
        * to search the invoices under your company1
    3. entering /invoice_search/company1/invoice1 will render InvoiceDisplayComponent
        * to display the invoice you are looking for
    4. if you add more stuff behind, it will render an error message instead.
* currently there are no buttons in invoice_search, so change the url directly to render the different outcomes


## To delete when project is done
### FE git workflow
1. Check you are starting from the correct branch (frontend) by doing 'git branch'
    * if not, use ```git checkout frontend``` to navigate to correct branch
    * once in ```frontend``` branch, do ```git pull```
        * doing ```git fetch``` followed by ```git merge``` does the same thing.

2. Before you start your own work, do ensure to do things from your own working branch.
    * create branch using ```git branch <child_branch> <parent_branch>```
    * for instance, if i want to create a branch called ```david``` from ```frontend```, I would do ```git branch david frontend```
    * navigate to your branch using ```git checkout david```
3. Stage file using ```git add <file1> <file2>```. Don't use ```git add .``` unless you only have edited/added files to be commited.
4. Commit with meaning messages using ```git commit -m "message"```
5. At this stage, all commits should have only been your own working local branch. ie ```david``` branch only exisit on your local repo. The next step is merging any conflicts from ```origin/frontend```, ie the frontend branch on remote or github.
    * go back to your local frontend branch using ```git checkout frontend```.
    * ```git pull``` to bring in any changes on origin/frontend onto your local frontend branch.
    * switch back to your own local working branch using ```checkout david```.
    * ```git rebase frontend``` to bring changes on local frontend branch to local working branch. 
    * resolve any conflicts you might have.
    * if there are changes in origin/main that you need in your work, its more complicated, so point it out so we can figure out together.
6. Once you are sure that there are no more conflicts, we will bring our changes to frontend branch:
    * switch to frontend branch using ```git checkout frontend```
    * rebase frontend using your working branch ```git rebase david```
    * merge and resolve any conflicts you might have
    * once you are sure nothing is wrong, publish branch to github. and pray.

### Learning points regarding debugging ocr
* check image file
* check internet connection
