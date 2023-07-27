export class BlogPostComponent {
  post = {
    title: '',
    description: '',
    image: null
  };

  constructor(private blogPostService: BlogPostService) {}

  createPost() {
    // Call the service method to create the post
    this.blogPostService.createPost(this.post).subscribe(
      response => {
        console.log(response);
        // Reset form fields
        this.post = {
          title: '',
          description: '',
          image: null
        };
      },
      error => {
        console.error(error);
      }
    );
  }

  handleImageUpload(event: any) {
    const file = event.target.files[0];
    // Handle the uploaded image (e.g., display preview)
    console.log(file);
    this.post.image = file;
  }
