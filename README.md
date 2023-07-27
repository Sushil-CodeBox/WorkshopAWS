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


  ----------------

  export class BlogPostService {
  private apiUrl = 'https://your-api-url.com/posts';

  constructor(private http: HttpClient) {}

  createPost(post: any): Observable<any> {
    const formData = new FormData();
    formData.append('title', post.title);
    formData.append('description', post.description);
    formData.append('image', post.image);

    return this.http.post(this.apiUrl, formData);
  }
}
