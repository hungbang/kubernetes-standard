76  git remote -v
   77  git add .
   78  git status
   79  git status
   80  git remote add origin https://hung_bang@bitbucket.org/hung_bang/smdmark.git
   81  git push origin master
   82  git remote set-url origin git@bitbucket.org:hung_bang/smdmark.git
   83  git push origin master
   84  git remote set-url origin https://hung_bang@bitbucket.org/hung_bang/smdmark.git
   85  git push origin master
   86  git status
   87  git add .
   88  git commit -m "Initial"
   89  git push origin master
   90  git status
   91  cd /usr/
   92  ls
   93  cd local/
   94  ls
   95  which flyway
   96  cd /usr/local/bin
   97  ls
   98  cd flyway 
   99  cd ..
  100  ls -l
  101  cd lib/
  102  ls -l
  103  history
  104  cd ..
  105  ls -l
  106  cd share/
  107  ls
  108  cd ..
  109  ls
  110  cd var/
  111  ls
  112  cd homebrew/
  113  ls
  114  cd ..
  115  cd ..
  116  cd ..
  117  ls
  118  cd lib
  119  ls
  120  cd ..
  121  ls
  122  cd libexec/
  123  ls
  124  where flyway
  125  which flyway
  126  cd /usr/
  127  ls
  128  cd bin/
  129  ls
  130  cd ..
  131  ls
  132  cd include/
  133  ls
  134  cd .
  135  cd ..
  136  ls -l
  137  cd lib
  138  ls
  139  cd ..
  140  ls
  141  cd local/
  142  ls
  143  cd Cellar/
  144  ls
  145  cd flyway/
  146  ls
  147  cd 5
  148  cd 5.1.4/
  149  ls -l
  150  cd libexec/
  151  ls
  152  cd sql/
  153  ls
  154  cd ..
  155  cd ..
  156  cd ..
  157  cd ..
  158  open flyway/
  159  ipfs cat /ipfs/QmbHpf6y6hVQ3wzk3A5rV4cPhtJNbai69hsLU8ssbPdcCc
  160  ipfs cat /ipfs/QmbHpf6y6hVQ3wzk3A5rV4cPhtJNbai69hsLU8ssbPdcCc/readme
  161  ipfs init
  162  cd /Users/hungbang/.ipfs
  163  ls
  164  cat config 
  165  cd ~
  166  ipfs swarm peers
  167  hash=`echo "I <3 -$(whoami)" | ipfs add -q`
  168  curl "ipfs.io/ipfs/$hash"
  169  curl "https://ipfs.io/ipfs/$hash"
  170  ipfs config --json API.HTTPHeaders.Access-Control-Allow-Origin "[\"*\"]"
  171  ipfs config --json API.HTTPHeaders.Access-Control-Allow-Credentials "[\"true\"]"
  172  cd Public/
  173  cd projects/
  174  cd smdmark/
  175  cd ..
  176  https://github.com/hungbang/js-ipfs-api.git
  177  https://github.com/hungbang/js-ipfs-api.git
  178  git clone https://github.com/hungbang/js-ipfs-api.git
  179  cd js-ipfs-api/
  180  npm install
  181  npm start
  182  ls
  183  cd examples/
  184  cd bundle-
  185  ls
  186  cd bundle-browserify/
  187  npm start
  188  npm install
  189  npm start
  190  ipfs daemon
  191  ipfs daemon
  192  ipfs daemon
  193  git status
  194  npm start
  195  cd frontend/
  196  npm start
  197  npm install
  198  npm start
  199  npm audit fix
  200  npm install
  201  npm start
  202  npm install
  203  npm audit fix
  204  npm start
  205  npm install rxjs-compat --save
  206  npm start
  207  npm start
  208  npm start
  209  npm install
  210  npm install
  211  npm start
  212  npm install ng6-toastr --save
  213  npm start
  214  npm start
  215  npm install
  216  npm start
  217  cd frontend/
  218  cd src/
  219  cd app/
  220  ls
  221  cd shared/
  222  cd services/
  223  ng g class modal.provider
  224  ng g class modal.service
  225  ng g class toast.provider
  226  cd ..
  227  cd utils/
  228  ng g class arrays.util
  229  cd ..
  230  cd modals/
  231  ng g class abstract.modal
  232  cd ..
  233  cd components/
  234  ng g component basic
  235  cd ..
  236  cd models/
  237  ng g class interfaces
  238  cd ..
  239  cd ..
  240  cd core/
  241  cd components/
  242  ng g class unsubscribe.component
  243  cd ..
  244  cd ..
  245  cd shared/
  246  cd services/
  247  cd ..
  248  cd ..
  249  cd core/
  250  mkdir services
  251  cd services/
  252  ng g class translate-loader.service
  253  cd ..
  254  ng g class core.module
  255  cd ..
  256  cd ..
  257  cd ..
  258  cd ..
  259  git status
  260  git status
  261  git rm -r --cached node_modules
  262  cd frontend/
  263  git rm -r --cached node_modules
  264  git commit -m "Remove node_modules now that they're ignored"
  265  git push origin master
  266  git rm -r --cached node_modules
  267  git commit -m "Remove node_modules now that they're ignored"
  268  git add .
  269  git commit -m "Remove node_modules now that they're ignored"
  270  git push origin master
  271  npm install
  272  npm start
  273  cd Public/
  274  cd projects/
  275  cd screening/
  276  docker-compose up --build -d backend
  277  ls
  278  cat .env 
  279  docker-compose up --build -d backend
  280  cd frontend/
  281  ng add @progress/kendo-angular-inputs
  282  npm install
  283  npm install
  284  ls -l
  285  cd frontend/
  286  cd src/
  287  cd app/
  288  cd products/
  289  ls
  290  cd components/
  291  ls
  292  ng g c product
  293  cd ..
  294  cd ..
  295  cd .
  296  cd ..
  297  cd ..
  298  npm start
  299  npm start
  300  npm start
  301  cd Public/projects/
  302  git clone https://github.com/hungbang/k8s-mastery.git
  303  cd k8s-mastery/
  304  cd sa-frontend/
  305  npm install
  306  npm start
  307  docker ps
  308  docker ps
  309  docker images 
  310  docker rmi -f $(docker images -f "dangling=true" -q)
  311  docker images 
  312  curl http://localhost:9200/_cluster/state?pretty
  313  curl http://localhost:9300/_cluster/state?pretty
  314  cd Public/projects/
  315  cd screening/
  316  ls
  317  docker-compose ps
  318  docker-compose up --build -d kibana
  319  docker-compose ps
  320  curl http://localhost:9200/_cluster/state?pretty
  321  docker-compose --help
  322  docker-compose down
  323  ls -l
  324  cat ingress.yaml 
  325  kubectl apply -f k8s-elasticsearch/
  326  kubectl get svc
  327  kubectl apply -f k8s-elasticsearch/
  328  kubectl apply -f k8s-elasticsearch/
  329  kubectl apply -f k8s-elasticsearch/
  330  kubectl apply -f k8s-elasticsearch/
  331  kubectl apply -f k8s-elasticsearch/
  332  kubectl apply -f k8s-elasticsearch/
  333  kubectl apply -f k8s-elasticsearch/
  334  kubectl get pods
  335  kubectl get svc
  336  kubectl help
  337  kubectl explain svc
  338  kubectl delete -f svc elasticsearch
  339  kubectl delete -f service elasticsearch
  340  kubectl delete svc elasticsearch
  341  kubectl apply -f k8s-elasticsearch/elasticsearch-service.yaml 
  342  kubectl explain svc elasticsearch
  343  kubectl delete svc elasticsearch
  344  kubectl apply -f k8s-elasticsearch/elasticsearch-service.yaml 
  345  kubectl get svc
  346  kubectl get pods
  347  kubectl logs -f pods
  348  kubectl logs -f elasticsearch
  349  kubectl logs -f elasticsearch
  350  kubectl get svc
  351  kubectl get pods
  352  kubectl apply -f k8s-elasticsearch/elasticsearch-deployment.yaml 
  353  kubectl get pods
  354  kubectl get svc
  355  kubectl get pods
  356  kubectl get pods
  357  kubectl delete svc elasticsearch
  358  kubectl apply -f k8s-elasticsearch/elasticsearch-service.yaml 
  359  kubectl get pods, svc, deployment -l component=elasticsearch
  360  kubectl get pods,svc,deployment -l component=elasticsearch
  361  kubectl get pods,svc,deployment
  362  curl http://10.105.132.63:9200
  363  kubectl delete pods,svc,deployment elasticsearch
  364  kubectl get pods,svc,deployment
  365  cd ..
  366  git clone https://github.com/hungbang/kubernetes-elasticsearch-cluster.git
  367  cd screening/
  368  kubectl apply -f k8s-elasticsearch/
  369  kubectl delete pods,svc,deployment elasticsearch
  370  kubectl get pods,svc,deployment
  371  kubectl get pods,svc,deployment
  372  kubectl get pods,svc,deployment
  373  kubectl get pods,svc,deployment
  374  kubectl ps
  375  kubectl get svc
  376  kubectl get svc
  377  defaults write com.apple.finder AppleShowAllFiles NO
  378  docker ps
  379  ipfs daemon
  380  ipfs config Addresses.API
  381  history
  382  which tslint
  383  cd /usr/local/
  384  ls
  385  cd ~
  386  cat /Users/hungbang/.npm/_logs/2018-10-27T00_51_14_246Z-debug.log
  387  node -v
  388  npm i ipfs
  389  yarn serve
  390  yarn serve
  391  cd Public/projects/screening/
  392  docker-compose ps
  393  docker-compose up --build -d backend
  394  docker logs -f backend
  395  docker logs -f ss-backend
  396  nano .env 
  397  docker-compose up --build -d backend
  398  docker logs -f ss-backend
  399  docker logs -f ss-backend
  400  docker-compose up --build -d backend
  401  docker-compose ps
  402  docker-compose up -d kibana
  403  docker-compose ps
  404  cd Public/projects/screening/
  405  docker-compose ps
  406  cd Public/projects/screening/
  407  ls
  408  cat .env 
  409  ipfs swarm peers
  410  ipfs swarm peers
  411  npm install ipscend --global
  412  ipfs daemon
  413  cd Public/projects/
  414  cd screening/
  415  ls
  416  docker-compose 
  417  docker-compose ps
  418  ipfs daemon
  419  ipfs swarm peers
  420  ipfs swarm peers
  421  npm install
  422  cd frontend/
  423  npm start
  424  npm start
  425  npm install @types/ipfs
  426  npm start
  427  npm start
  428  npm start
  429  npm start
  430  npm start
  431  cd backend/
  432  truffle develop
  433  rm -r build
  434  truffle compile
  435  migrate
  436  truffle develop
  437  cd frontend/
  438  npm start
  439  npm start
  440  npm start
  441  npm install --save ipfs-api
  442  npm start
  443  npm start
  444  cd backend/
  445  truffle develop
  446  ssh chuonghd@chuonghd.vantechdns.net
  447  cd Public/projects/screening/
  448  docker-compose ps
  449  cd ~
  450  python -V
  451  ls
  452  ./google-cloud-sdk/install.sh 
  453  cd .bash_profile 
  454  pwd
  455  kubectl get pods
  456  kubectl get pods,deploy
  457  kubectl delete deploy back
  458  kubectl get pod
  459  kubectl get pod
  460  kubectl get pods
  461  kubectl get pods
  462  kubectl delete pod backend-6c947c7c69-2xp2v
  463  kubectl get svc,pods,secret,deployment
  464  cd Public/projects/screening/
  465  kubectl apply -f k8s-backend/
  466  kubectl get svc,pods,secret,deployment
  467  kubectl get svc,pods,secret,deployment
  468  kubectl get svc,pods,secret,deployment
  469  kubectl logs -f backend-6c947c7c69-dqkgd
  470  kubectl describe pod backend-6c947c7c69-dqkgd
  471  kubectl describe secret ss-gce-access
  472  history
  473  kubectl create secret generic sanctionscreen-gcs-sccess --from-file=./configs/gce/SanctionScreen-GCS-Access.json 
  474  kubectl get svc,pods,secret,deployment
  475  kubectl describe secret sanctionscreen-gcs-sccess
  476  kubectl describe pod backend-6c947c7c69-dqkgd
  477  kubectl get svc,pods,secret,deployment
  478  kubectl describe pod backend-6c947c7c69-dqkgd
  479  docker-compose ps
  480  kubectl get pods
  481  kubectl logs -f backend-6c947c7c69-dqkgd
  482  cd Public/projects/screening/
  483  kubectl apply -f ingress.yaml 
  484  kubectl get svc,pods
  485  cd backend/
  486  pwd
  487  ls
  488  cd ..
  489  history
  490  kubectl get storageclasses --all-namespaces
  491  gcloud auth configure-docker 
  492  docker ps
  493  docker images
  494  cd Public/projects/screening/
  495  kubectl get pods
  496  kubectl get pods
  497  kubectl describe pod elasticsearch-57668d4b8c-bf7jh
  498  kubectl describe pod elasticsearch-57668d4b8c-bf7jh
  499  kubectl get pods
  500  kubectl logs elasticsearch-57668d4b8c-bf7jh -p
  501  gcloud container clusters get-credentials cloud-build-screening
  502  gcloud container clusters get-credentials cloud-build-screening --zone=us-central1-b
  503  kubectl get pods
  504  kubectl logs elasticsearch-57668d4b8c-bf7jh -p
  505  kubectl logs -f elasticsearch-57668d4b8c-bf7jh
  506  kubectl get pods
  507  kubectl get clusterrolebinding
  508  gcloud info | grep Account
  509  cd Public/projects/screening/
  510  kubectl get deployment
  511  kubectl delete deployment elasticsearch
  512  kubectl get pods,svc,deployment
  513  kubectl get pods,svc,deployment
  514  kubectl apply -f k8s-elasticsearch/elasticsearch-deployment.yaml 
  515  kubectl get pods,svc,deployment
  516  kubectl get pods,svc,deployment
  517  kubectl describe pod elasticsearch-598ff57f45-5h7dd
  518  kubectl describe pod elasticsearch-598ff57f45-5h7dd
  519  kubectl get pods,svc,deployment
  520  kubectl get pods,svc,deployment
  521  kubectl logs -f elasticsearch-598ff57f45-5h7dd
  522  kubectl get pods,svc,deployment
  523  kubectl describe pod elasticsearch-598ff57f45-5h7dd
  524  kubectl get pods,svc,deployment
  525  kubectl logs -f elasticsearch-598ff57f45-5h7dd
  526  kubectl get pods,svc,deployment
  527  kubectl get pods,svc,deployment
  528  kubectl logs -f elasticsearch-598ff57f45-5h7dd
  529  kubeval k8s-elasticsearch/elasticsearch-deployment.yaml 
  530  kubectl logs -f elasticsearch-598ff57f45-5h7dd
  531  kubectl get deployment
  532  kubectl delete deployment elasticsearch
  533  kubectl get pods,svc,deployment
  534  kubectl get pods,svc,deployment
  535  kubectl apply -f k8s-elasticsearch/elasticsearch-deployment.yaml 
  536  kubectl get pods,svc,deployment
  537  kubectl get pods,svc,deployment
  538  kubectl get pods,svc,deployment
  539  curl http://104.197.65.235:9200
  540  curl http://localhost:9200/_cluster/state?pretty
  541* curl http://104.197.65.235:9200_cluster/state?pretty
  542  curl http://104.197.65.235:9200/_cluster/state?pretty
  543  kubectl apply -f k8s-backend/,k8s-frontend/
  544  kubectl get pods,svc,deployment
  545  kubectl describe backend-58cdf6cd6b-rqzpw
  546  kubectl describe pod  backend-58cdf6cd6b-rqzpw
  547  gcloud auth configure-docker 
  548  kubectl describe pod  backend-58cdf6cd6b-rqzpw
  549  kubectl get pods,svc,deployment
  550  kubectl delete pod backend
  551  kubectl delete deployment backend
  552  kubectl delete deployment frontend
  553  kubectl get pods,svc,deployment
  554  kubectl apply -f k8s-backend/,k8s-frontend/
  555  kubectl get pods,svc,deployment
  556  kubectl describe pod backend-58cdf6cd6b-rs2rs
  557  docker pull gcr.io/sanctionscreen/ss-backend
  558  docker pull gcr.io/sanctionscreen/ss-backend
  559  docker pull gcr.io/sanctionscreen/ss-backend
  560  docker pull gcr.io/sanctionscreen/ss-frontend:d2d695662f6b1df97a60de71192350de980000c1
  561  kubectl apply -f k8s-backend/backend-deployment.yaml,k8s-frontend/frontend-deployment.yaml 
  562  kubectl get pods,svc,deployment
  563  kubectl get pods,svc,deployment
  564  kubectl get pods,svc,deployment
  565  kubectl describe pod backend-9bcc7c9cf-2hmfd
  566  kubectl get secret
  567  kubectl apply -f k8s-backend/backend-deployment.yaml,k8s-frontend/frontend-deployment.yaml 
  568  kubectl describe pod backend-9bcc7c9cf-2hmfd
  569  kubectl get pods,svc,deployment
  570  kubectl describe pod frontend-99987c5b6-24hfh
  571  kubectl apply -f k8s-frontend/frontend-deployment.yaml 
  572  kubectl get pods,svc,deployment
  573  kubectl get svc,pvm,secret
  574  kubectl get svc,pvc,secret