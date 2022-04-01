# PhpStorm live templates for Drupal 
This repository includes live templates for PhpStorm specific for Drupal development.

**Share your Favorite Settings**! This isn't meant to be a readonly repository. Have something you love about your PhpStorm setup? Create a pull request and share it.

## Installation
1. Go to _PhpStorm Preferences | Tools | Settings Repository_
2. Add Read-only Source https://github.com/brentgees/phpstorm-live-templates-drupal
3. Restart PhpStorm
You can see and manage all the snippets under the Preferences | Editor | Live Templates

# Live templates
### Drupal Templates

#### db_select

database select

```php
$query = \Drupal::database()->select('field_name', 'alias');
$query->fields('alias', ['field_1', 'field_2']);
$result = $query->execute()->fetchAll();
```

#### dblog

Log to watchdog

```php
\Drupal::messenger()->addError($e->getMessage());
```

#### load_service

Load service

```php
/** @var \Drupal\ $service */
$service = \Drupal::service('service.name');
```

#### entity_view

Entity view

```php
$view_builder = \Drupal::entityTypeManager()->getViewBuilder($entity->getEntityTypeId());
$entityView = $view_builder->view($entity, 'teaser');
```

#### entity_load

Loads drupal entity

```php
\Drupal::entityTypeManager()->getStorage('node')->load($id);


```

#### drupal_set_message

Set message

```php
\Drupal::messenger()->addMessage('message');
```

#### db_select_2

entityQuery

```php
$query = \Drupal::entityQuery('node')
    ->condition('status', 1)
    ->condition('changed', REQUEST_TIME, '<')
    ->condition('title', 'cat', 'CONTAINS')
    ->condition('field_tags.entity.name', 'cats');

$nids = $query->execute();
```

#### t_attr

```php
'#attributes' => ['class' => ['$CLASS$']],
```

#### t_html

```php
[
  '#type' => 'html_tag',
  '#tag' => '$TAG$',
  '#value' => $VALUE$,
]
```

#### t_markup

```php
[
  '#type' => 'markup',
  '#markup' => $MARKUP$,
 ]
```

#### t_link

```php
[
  '#type' => 'link',
  '#title' => $this->t('$TITLE$'),
  '#url' => Url::fromRoute('$ROUTE$', []),
  '#attributes' => [
    'class' => ['$CLASS$'],
  ],
]
```

#### t_links

```php
[
  '#theme' => 'links',
  '#links' => [
    [
      'title' => $this->t('$TITLE$'),
      'url' => Url::fromRoute('$ROUTE$', []),
      'attributes' => ['class' => ['$CLASS$']],
    ],
  ],
]
```

#### h_theme

```php
/**
 * Implements hook_theme().
 */
function $MODULE$_theme() {
  return [
    '$THEME$' => [
      'variables' => [
        '$VARIABLE$' => NULL,
      ],
    ],
  ];
}
```

#### t_container

```php
[
  '#type' => 'container',
  '#attributes' => ['class' => ['$CLASS$']],
  '#children' => [
    $CHILDREN$
  ],
]
```

#### t_select

```php
[
  '#type' => 'select',
  '#title' => $this->t('$LABEL$'),
  '#options' => [
    '$KEY$' => $this->t('$OPTION$'),
  ],
]
```

#### h_page_att

```php
/**
 * Implements hook_page_attachments_alter().
 */
function $MODULE$_page_attachments_alter(array &$attachments) {
  
}
```

#### t_ds

```php
namespace Drupal\$MODULE_NAME$\Plugin\DsField;

use Drupal\ds\Plugin\DsField\DsFieldBase;
use Symfony\Component\DependencyInjection\ContainerInterface;

/**
 * Plugin that renders the $DESCRIPTION$.
 *
* @DsField(
 *   id = "$FIELDID$",
 *   title = @Translation("$TITLE$"),
 *   entity_type = "$ENTITY_TYPE$",
 *   provider = "$MODULE_NAME$"
 * )
 */
class $CLASSNAME$ extends DsFieldBase {

  /**
   * {@inheritdoc}
   */
  public function __construct(array $configuration, $plugin_id, $plugin_definition) {
    parent::__construct($configuration, $plugin_id, $plugin_definition);
  }

  /**
   * {@inheritdoc}
   */
  public static function create(ContainerInterface $container, array $configuration, $plugin_id, $plugin_definition) {
    return new static(
      $configuration,
      $plugin_id,
      $plugin_definition,
      $container->get('entity_type.manager')
    );
  }

  /**
   * {@inheritdoc}
   */
  public function build() {
  
  }

}

```

#### t_list

```php
[
  '#theme' => 'item_list',
  '#items' => [
    $ITEMS$,
  ],
]
```

#### entity_query

```php
$query = $this->entityTypeManager->getStorage('$ENTITY_TYPE$')->getQuery()
  ->condition('status', 1)
  ->sort('changed', 'DESC')
  ->range(0, 1)
  ->accessCheck(FALSE)
  ->execute();
```

#### t_inline_template

```php
[
  '#type' => 'inline_template',
  '#template' => '$TEMPLATE$',
  '#context' => [
    'name' => $VRIABLE$,
  ],
];
```

#### sql_query

```php
$connection = \Drupal::database();
$query = $connection->select('$TABLE$', '$ALIAS$');
$query->join('$JOIN_TABLE$', '$JOIN_ALIAS$', '$ALIAS$.$TABLE_FIELD$ = $JOIN_ALIAS$.$JOIN_FIELD$');
$query->condition('$ALIAS$.$CONDITION_FIELD$', $CONDITION_VALUE$);
$query->fields('$ALIAS$', ['$FIELD$']);
$query->orderBy('$ALIAS$.$ORDER_FIELD$', 'DESC');
$query->range($RANGE_START$, $RANGE_END$);
$results = $query->execute()->fetchAll();
```

#### term_create

Creates a taxonomy term

```php
$term = Term::create([
  'vid' => 'vocabulary_name',
  'langcode' => 'en',
  'name' => 'INSERT_TAGNAME',
  'description' => [
    'value' => '<p>My description.</p>',
    'format' => 'full_html',
  ],
  'weight' => -1,
  'parent' => array (0),
]);
$term->save();
```

#### load_class

Loads a class

```php
\Drupal::classResolver()
    ->getInstanceFromDefinition(ClassName::class)
    ->info();
```

#### extra_field

Creates a pseudo field the OO way

```php
/**
 * Implements hook_entity_extra_field_info().
 */
function $MODULE$_entity_extra_field_info() {
  $field_definitions = [
    FirstClassname::class,
    SecondClassname::class,
  ];

  $info_array = [];
  foreach ($field_definitions as $field_definition) {
    $info = \Drupal::classResolver()
      ->getInstanceFromDefinition($field_definition)
      ->info();
    $info_array = array_merge_recursive($info_array, $info);
  }

  return $info_array;
}

/**
 * Implements hook_ENTITY_TYPE_view().
 */
function $MODULE$_node_view(array &$build, Drupal\Core\Entity\EntityInterface $entity, Drupal\Core\Entity\Display\EntityViewDisplayInterface $display, $view_mode) {
  $field_definitions = [
    FirstClassname::class,
    SecondClassname::class,
  ];

  foreach ($field_definitions as $field_definition) {
    \Drupal::classResolver()
      ->getInstanceFromDefinition($field_definition)
      ->view($build, $entity, $display, $view_mode);
  }

  return $build;
}

// @todo: create a Class in src/ExtraField, add <?php to it and use extra_field_class in there.
```

#### extra_field_class

Creates the class for the pseudo field

```php
namespace Drupal\module_name\ExtraField;

use Drupal\Core\Entity\Display\EntityViewDisplayInterface;
use Drupal\Core\Entity\EntityInterface;

/**
 * Provides the extra_field_name extra field.
 */
class $CLASSNAME$ {

  /**
   * The name of the extra field.
   */
  const FIELD_NAME = 'field_name';

  /**
   * Method for module_name_entity_extra_field_info().
   */
  public function info() {
    $extra = [];
    $extra['node']['node_type']['display'][self::FIELD_NAME] = [
      'label' => t('insert_label_here'),
      'description' => t('insert_description_here'),
      'visible' => FALSE,
    ];
    return $extra;
  }

  /**
   * Method for module_name_node_view().
   */
  public function view(array &$build, EntityInterface $entity, EntityViewDisplayInterface $display, $view_mode) {
    if ($display->getComponent(self::FIELD_NAME)) {
      $build[self::FIELD_NAME] = [
        '#type' => 'markup',
        '#markup' => 'This is my custom content',
      ];
    }
  }

}

```

#### menu_item_create

Creates a menu item

```php
$items = array(
  '1' => 'Menuitem_1',
  '2' => 'Menuitem_2',
  '3' => 'Menuitem_3'
);

foreach($items as $nid => $title) {
  $menu_link = \Drupal\menu_link_content\Entity\MenuLinkContent:create([
    'title' => $title,
    'link' => ['uri' => 'internal:/node/' . $nid],
    'menu_name' => 'main',
    'expanded' => TRUE,
  ]);
  $menu_link->save();
```

#### import_content

Import default content

```php
/**
 * Import default content.
 */
function $MODULE$_deploy_create_default_items() {
  $files = [
    'filename',
  ];
  foreach ($files as $file) {
    $file_path = \Drupal::service('extension.list.module')->getPath('$MODULE$') . '/assets/' . $file . '.yml';
    \Drupal::service('single_content_sync.importer')
      ->importFromFile($file_path);
  }
}
```

#### create_image

Creates a media image item

```php
  $files = [
    'filename.png' => 'File Name',
  ];
  foreach ($files as $file => $file_description) {
    $file_data = file_get_contents(\Drupal::service('extension.list.module')->getPath('$MODULE$') . '/assets/images/' . $file);
    $directory = 'public://';
    \Drupal::service('file_system')
      ->prepareDirectory($directory, Drupal\Core\File\FileSystemInterface::CREATE_DIRECTORY);
    $file = \Drupal::service('file.repository')->writeData($file_data, 'public://' . $file, Drupal\Core\File\FileSystemInterface::EXISTS_REPLACE);
    $media = Drupal\media\Entity\Media::create([
      'bundle' => 'image',
      'uid' => 1,
      'field_media_image' => [
        'target_id' => $file->id(),
        'alt' => 'Team',
      ],
    ]);

    $media->setName($file_description)
      ->setPublished(TRUE)
      ->save();
  }
```

#### deploy_hook

Creates a deploy hook

```php
/**
 * Deploy hook for $FUNCTIONDESCRIPTION$
 */
function $MODULE$_deploy_$FUNCTION$() {
  
}
```

#### twig_xdebug

Twig xdebug breakpoint

```php
{{ breakpoint() }}
```

#### t_theme

Render api theme

```php
[
  '#theme' => 'links',
  '#links' => $links,
];
```



## Credits
Thanks to https://github.com/nicwortel and https://github.com/knpuniversity for some inspiration for the README and general structure.
