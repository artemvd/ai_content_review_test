# AI Content Review Test and Development

## What is this recipe for?

This recipe is for testing and development of the AI Content Review functionality. It provides a test setup for AI Content Review functionality to make development of the feature easier. Do not use this recipe for production. This recipe can be used only as inspiration for creating your own recipe or just to check how the AI Content Review functionality works.

## What will you get when applying the recipe?

Modules that will be install:

- ai_content_review and all its dependencies (AI Core, etc)
- ai_agents (this is needed as one of the review criteria is based on AI Agent)
- ai_agents_debugger (this is needed to debug the AI Agent)
- token_entity_render (this is needed to render the entity content to be used as context for AI Agent)

Content types that will be created:

- page (Basic Page)

AI Agents that will be created:

- SEO Review Agent (this agent will be used to review the content for SEO)

## Links to visit:

- `/admin/config/ai/content-review/rules` here you will find AI Content Review rules
- `/admin/config/ai/content-review/records` here you will find AI Content Review records (the full list)
- `/admin/config/ai/agents/seo_review/edit/form` here you will find SEO Review Agent configuration
- `/node/add/page` here you can add a new page
- `/node/1/edit` here you can edit the page
- `/node/1/ai-review` here you can view the AI Content Review records for the page
- `/node/1/ai-review/history` here you can view the AI Content Review history for the current page

The last two links are also available as the local task menu items on the node edit page.

For the links above `1` is the node id. You can change it to any other node id.

## How it works?

For agent based review rules it is required to have an AI Agent that uses tool "AI Content Review Result". This tool will make sure that the review results are in the correct format and can be processed by the AI Content Review module. Optionally you can use "AI Content Review Suggestion Item" tool to provide suggestions for improvement.

By default there is only 1 review plugin - "Agent Based Review". There are 2 suggestion plugins "Text replacement" and "General Recommendation".

There are 2 types of review records that are bundle plugins: "Internal" and "External" reviews. Internal is attached to the content entity in Drupal, for external the url field is added so that some remote source can be reviewed.

## How to apply the recipe?

You can either require this package with composer or git clone it to `recipes` folder in your drupal project root. 

To fetch the package with composer you need to add this repository to your composer.json file:

```json
{
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/artemvd/ai_content_review_test"
        }
    ]
}
```

Then you can run `composer require artemvd/ai_content_review_test:dev-main` to fetch the package.

Then you can use `drush` or `drupal` command to apply the recipe as usual.

```bash
drush recipe ../recipes/ai_content_review_test
```

It is recommended to clear the caches after the recipe is applied:

```bash
drush cr
```

This recipe assumes that you have a minimal Drupal installation, or standard Drupal installation with AI module installed. If you don't have AI module installed, it will be pulled and installed for you. In addition you need to have at least 1 AI Provider with support of `chat_with_tools` operation type. For example OpenAI, amazee.io, etc. 

If you have a content type `page` already installed and it is not from `standard` profile, you may need to adjust the recipe to use your content type instead of `page`.

## Demo content

This recipe also adds one demo page that can be used for testing if needed.