

  ![CI](./ci.png "CI")


CodeIgniter v.4 Snippets
========================
For Sublime Text 3




![CI4](https://img.shields.io/badge/CodeIgniter-v4-orange)
![CI4](https://img.shields.io/badge/SublimeText-3-orange)




Install
-------

---

### Sublime Text - Package Control or Clone/Download

When i'll add more snippets, the repo will be proposed as a Sublime Package, but until then you can clone or download it and place the folder inside '**SublimeText3\Packages\User**' folder.



CodeIgniter 4 Snippets, here we go...
--------
---

**Code** | **Renders** | **Tip**
---|---|---
 `[ci4m]` | Model | *Have inside the basics for db connection*
 ---|---|---

 `[ci4c]` | Controller | *With data loading from the model and view rendering*
 ---|---|---

 `[ci4l]` | Layout | *Naked skeleton, to work with the view below*
 ---|---|---

 `[ci4v]` | Vue | *Extending the layout above ^^*


---

### ``[ci4m]+Tab`` Model File

*Snippet file: CI4-Snippets/ci4-model.sublime-snippet
*Usual models location: App/Models/*

The meaning and use of the config settings are in the docs at <a href="https://codeigniter4.github.io/userguide/models/model.html" target="_blank">CI4 Docs> Modeling Data> Using CodeIgniter's Model</a>

The exemple function is from the official ["News section" tutorial](https://codeigniter4.github.io/userguide/tutorial/news_section.html).

```php
<?php namespace ${1:App}\Models;

use CodeIgniter\Model;

class ${2:News}Model extends Model
{
    protected \$table = '${3:news}';  
    protected \$primaryKey = 'id';

    protected $returnType = 'array';
    protected $useSoftDeletes = false;

    protected \$allowedFields = ['title', 'slug'];

	// protected $useTimestamps = false;
	// protected $createdField  = 'created_at';
	// protected $updatedField  = 'updated_at';
	// protected $deletedField  = 'deleted_at';

	// protected $validationRules    = [];
	// protected $validationMessages = [];
	// protected $skipValidation     = false;

    // Exemple function to retrive data
    public function get${2:News}(\$slug = false)
    {
        if (\$slug === false)
        {
            return \$this->orderBy('id', 'desc')->findAll();  // Get all records
        }
        return \$this->asArray()
                     ->where(['slug' => \$slug])
                     ->first();                               // or Get one record
    }

}
```


### ``[ci4c]+Tab`` Controller File

*Snippet file: CI4-Snippets/ci4-model.sublime-snippet
*Usual controllers location: App/Controllers/*

Keeped (commented) the basic stuff needed to get data from a Model, 
the exemple works with the News model from the official tutorial.

Read the [Controllers Doc](https://codeigniter4.github.io/userguide/incoming/controllers.html) for more details.

```php
<?php namespace ${1:App}\Controllers;

use CodeIgniter\Controller;
//use App\Models\NewsModel;

class ${2:News} extends Controller
{
    public function index()
    {
        //\$model = new NewsModel();

            \$data = [
                //'news'  => $model->getNews(),
                'title' => 'Some title',
            ];

         echo view('${3:news}/${4:index}', $data);        
    }      
}
```



### ``[ci4l]+Tab`` Layouts

*Snippet file: CI4-Snippets/ci4-layout.sublime-snippet
*Usual layouts location: App/Views/Layouts/*

Basically an HTML skeleton with at least one 'section' inside, 
acting like a placeholder into the views extended from the layout.

```php
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8"/>
	<title>Layout</title>
</head>
<body>
	<?= $this->renderSection('content') ?>
</body>
</html>
```

### ```[ci4v]+Tab``` View

*Snippet file: CI4-Snippets/ci4-view.sublime-snippet
*Usual models location: App/Views/*

Filling up the sections defined into the layout.

```php
<?= \$this->extend('${1:layouts/main}') ?>


<?= \$this->section('${2:content}') ?>    

${3:content goes here}

<?= \$this->endSection() ?>
```


License
-------

Copyright 2019, Andrei Curelaru <andrei@andikod.fr>

MIT