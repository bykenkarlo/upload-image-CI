# Upload-Image-CI


public function __construct() {
		parent::__construct();
		$this->load->model('model_name');
		$this->load->library('encryption');
		$this->load->helper(array('form', 'url'));
		$this->load->library('upload');
	}
 
public function upload_file() {
  $fileData = array();
        // File upload script
            $this->upload->initialize(array(
            'upload_path' => './assets/images/ico/',
            'overwrite' => false,
            'max_filename' => 300,
            'encrypt_name' => true,
            'remove_spaces' => true,
            'allowed_types' => 'jpg|png|jpeg',
            'max_size' => 2048000,
            'xss_clean' => true,
            'max_width' => 800,
            'max_height' => 800,
        ));

        if(!$this->upload->do_upload('ico_img')) {
	        $error = array('error' => $this->upload->display_errors());
	        $this->load->view('location', $error);
        }
        else {
            $dataImg = $this->upload->data('file_name');
            $data = array('image_file'=>$dataImg);
            $this->model->insertImageMethod($data);
            redirect('location');
        }
}
