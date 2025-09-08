Source code for my personal site and tech certification blog -- techstudybuddy.net

There are three technical components that went into creating and administering the site itself.

Let's dive in!

### Initial site design and migration to Jekyll
I first chose a Bootstrap template that I liked. The format of my header, footer, landing page, and article previews are very close to the original in terms of formatting. I changed the fonts, colors, and sizing, which was all quite easy to do within style.css. I wound up scrapping well over half of what the template provided as it just wasn't relevant to what I wanted.

When it came to...

...designing the gradients used across the site, I used [**canva.com**](canva.com)

...deciding on a standard color palette, I used [**coolors.co**](coolors.co)

...picking custom icons for the favicon and footer icons, I used [**flaticon.com**](flaticon.com)

...choosing a custom font for all text, I used [**fontawesome.com**](fontawesome.com)

...selecting stock photos for the blog posts, I used [**freepik.com**](freepik.com)

Now all of this took place on my local machine. I was getting ready to host it, but adding new blog posts would be entirely too cumbersome without something like a [**static site generator**](https://www.cloudflare.com/learning/performance/static-site-generator/).

I evaluated all of the options and ultimately went with Jekyll. Migrating the site to Jekyll wasn't too difficult. I wrote about that experience [**here**](https://techstudybuddy.net/posts/blog/how-its-built/). This meant that adding new pages to the site would take a fraction of the time, and opened me up to some options for automation down the line.

### Hosting the site online
This is one of the few Jekyll sites that isn't hosted with GitHub Pages. This was still incredibly easy to set up. Not as easy as setting up a Shopify site or using some other browser-based website builder, but it was still very easy. If you want to host a static site online, you can get it up and running on AWS in no time with S3 static site hosting and Route 53's domain registration. And use a CDN like CloudFront to ensure that it rapidly loads for your users!

[These are mostly the same steps I took](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html).

After getting it hosted online, I then used the Google Search Console to ensure that it would be indexed by the search engine. There was a simple verification check that I had to complete by adding required information to Route 53. After that, I was able to see my site in search results.

### Adding a GitHub Actions workflow to automate builds and deploys
So now that the site is built with Jekyll and hosted on AWS, the only other thing I wanted to do to before considering this project's setup complete was to set up a simple CI/CD workflow. Now if this was a more complex project, this would be a much larger undertaking. We're talking separate environments, automated testing, semantic versioning, etc. But it's just a simple blog and personal site. So my CI/CD pipeline is a single yaml file in a single GitHub Actions workflow.

One of the issues I was having before the workflow was dealing with manual Jekyll builds and artifact uploads to S3. I wanted this automated every time there was a change to the site. 

Because I was using Jekyll, I was able to find a template for building the site. I then added onto it so that it would output the generated site files to a separate branch, push that branch to S3, and then invalidate the CloudFront cache so the changes would be live. Other than adding onto the yaml file, I had to add three repository secrets to make sure this worked. Two were for my AWS access key and key ID and the other was for my CloudFront distribution name. I also had to modify the built-in GITHUB_TOKEN permissions so that it would be able to post the site contents to the separate branch.

### Maintaining the site
At this point, I consider the design and set up of the site to be complete. I am happy with where it is, although I may add a separate workflow step to validate that there are no dead links with any of the embedded hyperlinks in my site. 

I'm now focused on generating content for my site. This means passing more certification exams so that I can share my experiences. 

Thanks for reading and please reach out to me on LinkedIn if you have any questions!
