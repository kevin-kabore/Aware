-- Create the express app in the correct repo
  -express -e api or backend (your backend)
  -cd & npm install
  - make github repo

-- Set up app config
  -change app.js to server.js
  -go into bin file and change app link to server
  -one routes file in config/routes.js & delete routes folder
    delete users routes
  -connect to database using mongooose
    req mongoose (npm install also)
    database file (check bootsy & edit variables)
    make .env file (npm install also)
      LOCAL_DB=databaseName
      require in server.js require(dotenv).config()
      in server.js var mongoose = require('./config/database')
    add .gitignore  and add .env and node_modules to it (copy code from some other project)
  -adjust error handling middleware
    render json in server.js instead of ejs templates
  -commit after setting up config
-- Create Angular frontend
    -Make folder, cd and touch index.html
    -create and link app.js. mkdir css/styles.js and js/app.js
    -srcipt tags for all (check other projects)
    -require app.js in script tag by your closing body tags
    -can npm install http-server -s
    -Check that working in browser
    -define angular module, connect in ng-app
    -commit

-- Go through user stories
-- Make landing page
    -Connect UI router
    -create and link routes files
    -create home state
    -render home template in index

    -Make frontend config file & touch routes file + connect with script tag
    -in routes file
      -Make angular config module and inject $stateProvider, $urlRouterProvider
      -in function, create first state for home
      function MainRoutes($stateProvider, $urlRouterProvider){
        $stateProvider
          .state('home',{
            url: '/',
            templateUrl: '/templates/home.html'
            });
      }
      -inject ui.router to app.js
      -make actual template forlder and 'home.html'
    -make <main class='container' ui-view> for your views and import ui.view in your index file
    -commit and push

-- Branch always Branch when you start a new feature
  -git checkout -b branch_name
  -git commit
  -git checkout master
  -git merge branch_name
  -git push origin master
  -git checkout new_branch_name

-- Make models
  -model requires mongoose and schema
  -make model and export
  -create Seeds
    config/seeds.js
    check an example
    require('dotenv').load();
  -test seeds
    go into mongo
    show dbs, use db_name, db.model_name.find()

-- Check that you can see data

  -Create routes
  -router.route('/api/games')
    .get(gamesController.index)
    check criminals lab to see functionality of the select
  -require controller, then make controller & make index function
    make proper requires (check examples)
  -test in postman make sure you required database after requiring .env file
  -git commit
  -git checkout master
  -git merge branch_name
  -git push origin master
  -git checkout new_branch_name

  -Bring in $resource Frontend
    inject ngResource to app.js as dependency
  -Create game resource
    -make resources folder in js/games/game.resource.js
    -modularize. Put all the necessary code for all the games in the games folder
    angular.module('')
      .factory('GameResource', 'GameResource');
    inject($resource)
    function GameResource($resource){
      return $resource('http://localhost:3000/api/games', {id: '@_id'}, {'update': {method: {'PATCH'}}})
    }
  -add state to uiRouter under home state
    .state('gamesList', {
      url: '/games/list',
      templateUrl: 'games/show-list.html',
      controller: 'GamesListController',
      controllerAs: 'gamesListCtrl'
      })
  -make games-list.html template in js/games
  -in js/games folder make games.controller
    inside, make GamesListController as module
      inject GameResource
      function GamesListController(GameResource) {
        var self = this;
        self.game = [];
        GameResource.query().$promise.then(function(resp){
          self.games = resp.data.games
          })
      }
    -require the controller as script file in index
  -allow Cors stuff in app.js
    from authentication lab
  -ng-repeat in games-list.html (ui-router already gives you the controller Alias)
    <li  ng-repeat="game in gamesListCtrl.games">{{game.nameOrWhaterverProperty}} </li>

--Back to backend and make your other routes and functions
--Back to frontend to make controllers and templates. Make ALL controllers in games.controllerS.js file
