## Hi there 👋
Skip to content

Code
Issues
Pull requests
More
Supreme-phantom

 0 stars
 0 forks
 1 watching
 Activity
Public repository
Jitkaplatform/MASTER
 Branches
 Tags
Latest commit
@Jitkaplatform
Jitkaplatform
…
3 hours ago
Git stats
Files
README.md
MASTER
Supreme-phantom DIGITAL•=•OWNER=•JUAN•DIEGO•MENDOZA•CHAVEZ ANALOG•==•OWNER=•JUAN•DIEGO•MENDOZA•CHAVEZ (JUAN•DIEGO•MENDOZA•CHAVEZ) AUTHOR'S NAME(MAKE) •=(JUAN•DIEGO•MENDOZA•CHAVEZ) following owner allowed to all rights + privileges•= Skip to content

Code Issues 49 More Comparing changes Choose two branches to see what’s changed or to start a new pull request. If you need to, you can also .

...

Able to merge. These branches can be automatically merged. An owner of this repository has limited the ability to open a pull request from new users. 1 commit 1 file changed 1 contributor Commits on Oct 7, 2023 Update working-with-the-rubygems-registry.md

@Jitkaplatform Jitkaplatform committed 1 minute ago Showing with 25 additions and 0 deletions. 25 changes: 25 additions & 0 deletions25
...s/working-with-a-github-packages-registry/working-with-the-rubygems-registry.md @@ -1,3 +1,28 @@ Skip to content

Code Issues Pull requests More BreadcrumbsMASTER /README.md Latest commit Jitkaplatform Jitkaplatform 7 minutes ago History 12 lines (9 loc) · 309 Bytes File metadata and controls

Preview

Code

Blame MASTER Supreme-phantom DIGITAL•=•OWNER=•JUAN•DIEGO•MENDOZA•CHAVEZ ANALOG•==•OWNER=•JUAN•DIEGO•MENDOZA•CHAVEZ (JUAN•DIEGO•MENDOZA•CHAVEZ) AUTHOR'S NAME(MAKE) •=(JUAN•DIEGO•MENDOZA•CHAVEZ) following owner allowed to all rights + privileges•=

utf-⁸⁸chrome_image_Oct 6, 2023 10_48_13 AM PDT
title: Working with the RubyGems registry intro: 'You can configure RubyGems to publish a package to {% data variables.product.prodname_registry %} and to use packages stored on {% data variables.product.prodname_registry %} as dependencies in a Ruby project with Bundler.' product: '{% data reusables.gated-features.packages %}' redirect_from:

/articles/configuring-rubygems-for-use-with-github-package-registry
/github/managing-packages-with-github-package-registry/configuring-rubygems-for-use-with-github-package-registry
/github/managing-packages-with-github-packages/configuring-rubygems-for-use-with-github-packages
/packages/using-github-packages-with-your-projects-ecosystem/configuring-rubygems-for-use-with-github-packages
/packages/guides/configuring-rubygems-for-use-with-github-packages versions: fpt: '' ghes: '' ghae: '' ghec: '' shortTitle: RubyGems registry
{% data reusables.package_registry.packages-ghes-release-stage %} {% data reusables.package_registry.packages-ghae-release-stage %} {% data reusables.package_registry.admins-can-configure-package-types %}

Prerequisites
You must have RubyGems 2.4.1 or higher. To find your RubyGems version:
gem --version
You must have bundler 1.6.4 or higher. To find your Bundler version:
$ bundle --version
Bundler version 1.13.7
Authenticating to {% data variables.product.prodname_registry %}
{% data reusables.package_registry.authenticate-packages %} {% ifversion packages-rubygems-v2 %}

Authenticating in a {% data variables.product.prodname_actions %} workflow
This registry supports granular permissions. {% data reusables.package_registry.authenticate_with_pat_for_v2_registry %} {% data reusables.package_registry.v2-actions-codespaces %} {% endif %}

Authenticating with a {% data variables.product.pat_generic %}
{% data reusables.package_registry.required-scopes %} To publish and install gems, you can configure RubyGems or Bundler to authenticate to {% data variables.product.prodname_registry %} using your {% data variables.product.pat_generic %}. To publish new gems, you need to authenticate to {% data variables.product.prodname_registry %} with RubyGems by editing your ~/.gem/credentials file to include your {% data variables.product.pat_v1 %}. Create a new ~/.gem/credentials file if this file doesn't exist. For example, you would create or edit a ~/.gem/credentials to include the following, replacing TOKEN with your {% data variables.product.pat_generic %}.

---
:github: Bearer TOKEN
To install gems, you need to authenticate to {% data variables.product.prodname_registry %} by updating your gem sources to include https://USERNAME:TOKEN@{% ifversion fpt or ghec %}rubygems.pkg.github.com{% else %}REGISTRY_URL{% endif %}/NAMESPACE/. You must replace:

USERNAME with your {% data variables.product.prodname_dotcom %} username.
TOKEN with your {% data variables.product.pat_v1 %}.
NAMESPACE with the name of the personal account or organization {% ifversion packages-rubygems-v2 %}to which the gem is scoped{% else %}that owns the repository containing the gem{% endif %}.{% ifversion ghes %}
REGISTRY_URL with the URL for your instance's Rubygems registry. If your instance has subdomain isolation enabled, use rubygems.HOSTNAME. If your instance has subdomain isolation disabled, use HOSTNAME/_registry/rubygems. In either case, replace HOSTNAME with the hostname of your {% data variables.product.prodname_ghe_server %} instance. {% elsif ghae %}
REGISTRY_URL with the URL for your instance's Rubygems registry, rubygems.HOSTNAME. Replace HOSTNAME with the hostname of {% data variables.location.product_location %}. {% endif %} If you would like your package to be available globally, you can run the following command to add your registry as a source.
gem sources --add https://USERNAME:TOKEN@{% ifversion fpt or ghec %}rubygems.pkg.github.com{% else %}REGISTRY_URL{% endif %}/NAMESPACE/
To authenticate with Bundler, configure Bundler to use your {% data variables.product.pat_v1 %}, replacing USERNAME with your {% data variables.product.prodname_dotcom %} username, TOKEN with your {% data variables.product.pat_generic %}, and NAMESPACE with the name of the personal account or organization {% ifversion packages-rubygems-v2 %}to which the gem is scoped{% else %}that owns the repository containing the gem{% endif %}.{% ifversion ghes %} Replace REGISTRY_URL with the URL for your instance's RubyGems registry. If your instance has subdomain isolation enabled, use rubygems.HOSTNAME. If your instance has subdomain isolation disabled, use HOSTNAME/_registry/rubygems. In either case, replace HOSTNAME with the hostname of your {% data variables.product.prodname_ghe_server %} instance.{% elsif ghae %}Replace REGISTRY_URL with the URL for your instance's Rubygems registry, rubygems.HOSTNAME. Replace HOSTNAME with the hostname of {% data variables.location.product_location %}.{% endif %}

bundle config https://{% ifversion fpt or ghec %}rubygems.pkg.github.com{% else %}REGISTRY_URL{% endif %}/NAMESPACE USERNAME:TOKEN
Publishing a package
{% ifversion packages-rubygems-v2 %}{% data reusables.package_registry.publishing-user-scoped-packages %}{% else %}By default, GitHub publishes the package to an existing repository with the same name as the package. For example, when you publish GEM_NAME to the octo-org organization, GitHub Packages publishes the gem to the octo-org/GEM_NAME repository.{% endif %} For more information on creating your gem, see "Make your own gem" in the RubyGems documentation. {% data reusables.package_registry.auto-inherit-permissions-note %} {% data reusables.package_registry.authenticate-step %}

Build the package from the gemspec to create the .gem package. Replace GEM_NAME with the name of your gem.
gem build GEM_NAME.gemspec
Publish a package to {% data variables.product.prodname_registry %}, replacing NAMESPACE with the name of the personal account or organization {% ifversion packages-rubygems-v2 %}to which the package will be scoped{% else %}that owns the repository containing your project{% endif %} and GEM_NAME with the name of your gem package.{% ifversion ghes %} Replace REGISTRY_URL with the URL for your instance's Rubygems registry. If your instance has subdomain isolation enabled, use rubygems.HOSTNAME. If your instance has subdomain isolation disabled, use HOSTNAME/_registry/rubygems. In either case, replace HOSTNAME with the host name of your {% data variables.product.prodname_ghe_server %} instance.{% elsif ghae %} Replace REGISTRY_URL with the URL for your instance's Rubygems registry, rubygems.HOSTNAME. Replace HOSTNAME with the hostname of {% data variables.location.product_location %}.{% endif %} {% note %} Note: The maximum uncompressed size of a gem's metadata.gz file must be less than {% data variables.package_registry.limit_rubygems_max_metadata_size %}. Requests to push gems that exceed that limit will fail. {% endnote %}
$ gem push --key github \
--host https://{% ifversion fpt or ghec %}rubygems.pkg.github.com{% else %}REGISTRY_URL{% endif %}/NAMESPACE \
GEM_NAME-0.0.1.gem
{% ifversion packages-rubygems-v2 %}

Connecting a package to a repository
The RubyGems registry stores packages within your organization or personal account, and allows you to associate packages with a repository. You can choose whether to inherit permissions from a repository, or set granular permissions independently of a repository. You can ensure gems will be linked to a repository as soon as they are published by including the URL of the {% data variables.product.prodname_dotcom %} repository in the github_repo field in gem.metadata. You can link multiple gems to the same repository. {% ifversion ghes %} In the following example, replace HOSTNAME with the host name of {% data variables.location.product_location %}.{% endif %}

gem.metadata = { "github_repo" => "ssh://{% ifversion fpt or ghec %}github.com{% else %}HOSTNAME{% endif %}/OWNER/REPOSITORY" }
For information on linking a published package with a repository, see "AUTOTITLE." {% else %}

Publishing multiple packages to the same repository
To publish multiple gems to the same repository, you can include the URL to the {% data variables.product.prodname_dotcom %} repository in the github_repo field in gem.metadata. If you include this field, {% data variables.product.prodname_dotcom %} matches the repository based on this value, instead of using the gem name.{% ifversion ghes or ghae %} Replace HOSTNAME with the host name of {% data variables.location.product_location %}.{% endif %}

gem.metadata = { "github_repo" => "ssh://{% ifversion fpt or ghec %}github.com{% else %}HOSTNAME{% endif %}/OWNER/REPOSITORY" }
{% endif %}

Installing a package
You can use gems from {% data variables.product.prodname_registry %} much like you use gems from rubygems.org. You need to authenticate to {% data variables.product.prodname_registry %} by adding your {% data variables.product.prodname_dotcom %} user or organization as a source in the ~/.gemrc file or by using Bundler and editing your Gemfile. {% data reusables.package_registry.authenticate-step %}

For Bundler, add your {% data variables.product.prodname_dotcom %} user or organization as a source in your Gemfile to fetch gems from this new source. For example, you can add a new source block to your Gemfile that uses {% data variables.product.prodname_registry %} only for the packages you specify, replacing GEM_NAME with the package you want to install from {% data variables.product.prodname_registry %} and NAMESPACE with the personal account or organization {% ifversion packages-rubygems-v2 %}to which the gem you want to install is scoped{% else %}that owns the repository containing the gem you want to install{% endif %}.{% ifversion ghes %} Replace REGISTRY_URL with the URL for your instance's Rubygems registry. If your instance has subdomain isolation enabled, use rubygems.HOSTNAME. If your instance has subdomain isolation disabled, use HOSTNAME/_registry/rubygems. In either case, replace HOSTNAME with the host name of your {% data variables.product.prodname_ghe_server %} instance.{% elsif ghae %} Replace REGISTRY_URL with the URL for your instance's Rubygems registry, rubygems.HOSTNAME. Replace HOSTNAME with the hostname of {% data variables.location.product_location %}.{% endif %}
source "https://rubygems.org"
gem "rails"
source "https://{% ifversion fpt or ghec %}rubygems.pkg.github.com{% else %}REGISTRY_URL{% endif %}/NAMESPACE" do
  gem "GEM_NAME"
end
For Bundler versions earlier than 1.7.0, you need to add a new global source. For more information on using Bundler, see the bundler.io documentation.
source "https://{% ifversion fpt or ghec %}rubygems.pkg.github.com{% else %}REGISTRY_URL{% endif %}/NAMESPACE"
source "https://rubygems.org"
gem "rails"
gem "GEM_NAME"
Install the package:
gem install GEM_NAME --version "0.1.1"
Further reading
"AUTOTITLE" Footer © 2023 GitHub, Inc. Footer navigation Terms Privacy Security Status Docs Contact GitHub Pricing API Training Blog About
utf-⁸⁸
Releases
No releases published
Create a new release
Packages
No packages published
Publish your first package
Footer
© 2023 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
