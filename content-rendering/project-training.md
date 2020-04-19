# Scaffolding
![Project scaffolding](../images/project-scaffolding.png)

# Hello world
1. In components folder create two folder content, for specific components, and structure for structure template
2. In structure create a components with properties like the screenshot
![Contentpage component](../images/contentpage-componets.png)
3. Rename contentpage.jsp to contentpage.html with the codes:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Training Homepage</title>
</head>
<body>
    <h1>Hello world</h1>
</body>
</html>
```
4. Create templates folder in apps/training
5. In /content folder create nt:unstructured node with name hello-world
6. In hello-world node added property: ``sling:resourceType - String - training/components/structure/contentpage```
7. Go to (hello-world component)[http://localhost:4502/content/hello-world.html]
![hello-world component](../images/hello-world-component.png)
