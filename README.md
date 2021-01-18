*Looking for a shareable component template? Go here --> [sveltejs/component-template](https://github.com/sveltejs/component-template)*

---

# KNMI No2

This project is to Comparing the NO2 air pollution during COVID-19 in different cities to see what measures help most in reducing air pollution.


## Where are the datasets from?

Getting images from [Google Earth engine](https://earthengine.google.com/)

Messurements from [Europe](#)

Getting the NO2 data for making graphs [Google Earth engine](https://earthengine.google.com/)

```js
var startDate = '2019-01-01';
var endDate = '2020-12-31';
var weekDifference = ee.Date(startDate).advance(1, 'week').millis().subtract(ee.Date(startDate).millis());
var listMap = ee.List.sequence(ee.Date(startDate).millis(), ee.Date(endDate).millis(), weekDifference)

function getWeeklyData(date) {
  var collection = ee.ImageCollection('COPERNICUS/S5P/NRTI/L3_NO2')
  .select('tropospheric_NO2_column_number_density')
  .filterDate(date, date.advance(1, 'week'))
  .filterBounds(geometry)
  
  var mean = collection.mean()
  var reducers = ee.Reducer.mean();
  
  //reproject the image to get a correct CRS
  var reprojected = mean
  .unitScale(0,1)
  .reproject('EPSG:4326', null, 100)
  
  //Use the combined reducer to get the mean and SD of the image
  var stats = reprojected.reduceRegion({
    reducer: reducers,
    bestEffort: true,
    geometry: geometry
  });
  
  return {
    date: date,
    number: stats.get('tropospheric_NO2_column_number_density')
  };
}

var data = listMap.map(function(dateMillis) {
  var date = ee.Date(dateMillis);
  return getWeeklyData(date)
});

print(data)

```

Got help from the other team from Stan & Jordy

### Team

Rowin Ruizendaal
Nienke Cornielje
Youri Stil



### How to install

This is a project template for [Svelte](https://svelte.dev) apps. It lives at https://github.com/sveltejs/template.

To create a new project based on this template using [degit](https://github.com/Rich-Harris/degit):

```bash
npx degit sveltejs/template svelte-app
cd svelte-app
```

*Note that you will need to have [Node.js](https://nodejs.org) installed.*


## Get started

Install the dependencies...

```bash
cd svelte-app
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).


## Single-page app mode

By default, sirv will only respond to requests that match files in `public`. This is to maximise compatibility with static fileservers, allowing you to deploy your app anywhere.

If you're building a single-page app (SPA) with multiple routes, sirv needs to be able to respond to requests for *any* path. You can make it so by editing the `"start"` command in package.json:

```js
"start": "sirv public --single"
```

## Using TypeScript

This template comes with a script to set up a TypeScript development environment, you can run it immediately after cloning the template with:

```bash
node scripts/setupTypeScript.js
```

Or remove the script via:

```bash
rm scripts/setupTypeScript.js
```

## Deploying to the web

### With [Vercel](https://vercel.com)

Install `vercel` if you haven't already:

```bash
npm install -g vercel
```

Then, from within your project folder:

```bash
cd public
vercel deploy --name my-project
```

### With [surge](https://surge.sh/)

Install `surge` if you haven't already:

```bash
npm install -g surge
```

Then, from within your project folder:

```bash
npm run build
surge public my-project.surge.sh
```
