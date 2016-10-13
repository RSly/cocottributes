# cocottributes
Code use to create COCO Attributes dataset and experiments in the associate ECCV 2016 paper. 

# instructions for starting the server
sudo service nginx start
uwsgi --socket 127.0.0.1:8081 -w wsgi:app

# instructions for starting mturk hits

manage_hits.py
    '''
    returns list of job_ids that have less than 3 hits by trusted workers
    job_id occur multiple times if missing multiple hits
    '''
    get_missing_hits(job_type):
    
    launch_missing_hits(job_type, task_file, mturk_rel_path)

ela_hits.py
    # Note: this module is called by views.py, not by the requester directly in normal operation
    '''
    this is the number of questions permitted in the ELA
    '''
    NUMQ = 40
    '''
    func for adding (patch, attribute) question to Query table, check if enough queries to launch new hit
    for relaunching hits that already have labels
    '''
    schedule_next_query(patch_id, cat_id)

make_task.py
    '''
    Batches patch_ids into groups of 10 and attr_ids into groups of 20 
    Makes set of HITs
    allimgs=True for binary attribute labeling tasks with one image per query
    allimgs=False for multiple attribute annotation
    Output: list of job_ids created
    '''
    make_tasks(patch_ids, attr_ids, task_label, job_type='annotation', allimgs=False)

views.py:
    '''
    server function that runs when a form from the 'allimgs' page is submitted
    these are assumed to be ela tasks, and the ela function is queried after the annotations are logged
    '''
    allimgs_post(self, id)