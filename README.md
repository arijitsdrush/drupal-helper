
 **Drupal Hook_help Code**

function survey_help($route_name, RouteMatchInterface $route_match) {

  switch ($route_name) {
    case 'help.page.survey':
      $text = file_get_contents(dirname(__FILE__) . "/README.md");
      if (!\Drupal::moduleHandler()->moduleExists('markdown')) {
        return '<pre>' . $text . '</pre>';
      }
      else {
        // Use the Markdown filter to render the README.
        $filter_manager = \Drupal::service('plugin.manager.filter');
        $settings = \Drupal::configFactory()->get('markdown.settings')->getRawData();
        $config = ['settings' => $settings];
        $filter = $filter_manager->createInstance('markdown', $config);
        return $filter->process($text, 'en');
      }
  }
  return NULL;
}
