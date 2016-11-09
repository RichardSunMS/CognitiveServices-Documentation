<!-- 
NavPath: Content Moderator
LinkLabel: Video Moderation API
Url: content-moderator/documentation/video-moderation-api
Weight: 150
-->

# Video Moderation API #

Today, online viewers are generating billions of video views across popular and regional social media web sites and increasing. With proactive detection of adult content in your video files, you can significantly lower the cost of your moderation efforts. Furthermore, gaining this type of early insight can enable you to make better decisions and create safer experiences for your customers.

## How it works ##

The Content Moderator video moderation capability is powered by the adult content classifier running within Azure Media Services. The capability is currently in beta and available at no charge.

You will need to subscribe to the Azure Media Services though, and the free tier can help you to evaluate the video moderation with your content. Depending on your volumes and purchase options, your expenses will include storage and compute costs.

[Contact us](https://cognitive.uservoice.com/ "Contact Us") if you would like to try the video moderation capability.

## Code Sample ##

The following is a sample C# program set that will get you started with your first Content Moderator job. This code requires both the [Azure Media Services C# SDK](https://github.com/Azure/azure-sdk-for-media-services "Azure Media Services SDK") and [SDK Extensions packages](https://github.com/Azure/azure-sdk-for-media-services-extensions "SDK Extensions") (available on [NuGet](http://www.nuget.org/packages?q=Azure+Media+Services+.NET+SDK "Nuget")).

	
	using System;
	using System.Linq;
	using System;
	using System.Linq;
	using System.Threading.Tasks;
	using Microsoft.WindowsAzure.MediaServices.Client;
	using System.IO;
	using System.Threading;

	namespace ContentModeratorAmsSample
	{
    	class Program
    	{
        	// declare constants and globals
        	private static CloudMediaContext _context = null;
        	private static readonly string _accountName = { ACCOUNT_NAME };
        	private static readonly string _accountKey = { ACCOUNT_KEY };
        	private const string _mpName = "Azure Media Content Moderator";
        	private static readonly string _inputFile = { INPUT_FILE_PATH };
        	private static readonly string _outputFolder = { OUTPUT_FOLDER_PATH };

			//True if videos on the server should be scaled down false if not. 
        	//Scaling the video down has better performance but could have some impact on the scoring
        	
			private const bool _moderatorConfiguration = false;

        	static void Main(string[] args)
        	{
            	_context = new CloudMediaContext(_accountName, _accountKey);
            	RunContentModeratorJob(_inputFile, _outputFolder, _moderatorConfiguration);
        	}

			static void RunContentModeratorJob(string inputFilePath, string output, bool scaleVideo)
        	{

            	// create asset with input file
            	IAsset asset = _context.Assets.CreateFromFile(inputFilePath, AssetCreationOptions.None);
            
            	// grab instance of Azure Media Content Moderator MP
            	IMediaProcessor mp = _context.MediaProcessors.GetLatestMediaProcessorByName(_mpName);

            	// create Job with Content Moderator task
            	IJob job = _context.Jobs.Create(String.Format("Content Moderator {0}", 
                Path.GetFileName(inputFilePath) + "_" + Guid.NewGuid()));

           	 	ITask contentModeratorTask = job.Tasks.AddNew("Adult classifier task",
                	mp,
                	scaleVideo ? "sdv=true" : "sdv=false",
                	TaskOptions.None);

            	contentModeratorTask.InputAssets.Add(asset);
            	contentModeratorTask.OutputAssets.AddNew("Adult classifier output",
            	AssetCreationOptions.None);

            	job.Submit();

            	// Create progress printing and querying tasks
            	Task progressPrintTask = new Task(() =>
            	{
                	IJob jobQuery = null;
                	do
                	{
                    	var progressContext = _context;
                    	jobQuery = progressContext.Jobs
                    		.Where(j => j.Id == job.Id)
                    		.First();
                    
						Console.WriteLine(string.Format("{0}\t{1}",
                    	DateTime.Now,
                    	jobQuery.State));
                    	Thread.Sleep(10000);
                	}
                	while (jobQuery.State != JobState.Finished &&	                
						jobQuery.State != JobState.Error &&
                		jobQuery.State != JobState.Canceled);
            	});

				progressPrintTask.Start();

            	Task progressJobTask = job.GetExecutionProgressTask(
            		CancellationToken.None);
            	progressJobTask.Wait();

            	// If job state is Error, the event handling 
            	// method for job progress should log errors.  Here we check 
            	// for error state and exit if needed.
            	if (job.State == JobState.Error)
            	{
                	ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                	Console.WriteLine(string.Format("Error: {0}. {1}",
                	error.Code,
                	error.Message));
            	}

            	DownloadAsset(job.OutputMediaAssets.First(), output);
        	}

			static void DownloadAsset(IAsset asset, string outputDirectory)
        	{
            	foreach (IAssetFile file in asset.AssetFiles)
            	{
                	file.Download(Path.Combine(outputDirectory, file.Name));
            	}
        	}

			// event handler for Job State
        	static void StateChanged(object sender, JobStateChangedEventArgs e)
        	{
            	Console.WriteLine("Job state changed event:");
            	Console.WriteLine("  Previous state: " + e.PreviousState);
            	Console.WriteLine("  Current state: " + e.CurrentState);
            	switch (e.CurrentState)
            	{
                	case JobState.Finished:
                    	Console.WriteLine();
                    	Console.WriteLine("Job finished.");
                    	break;
                	case JobState.Canceling:
                	case JobState.Queued:
                	case JobState.Scheduled:
                	case JobState.Processing:
                    	Console.WriteLine("Please wait...\n");
                    	break;
                	case JobState.Canceled:
                    	Console.WriteLine("Job is canceled.\n");
                    	break;
                	case JobState.Error:
                    	Console.WriteLine("Job failed.\n");
                    	break;
                	default:
                    	break;
            	}
        	}
    	}
	}


## Sample Response (XML) ##

The same response includes:

- InputFileName: The name of the file, as saved on the input asset in Azure Media Services.
- FileSize: The size of the input file in bytes.
- AdultClassifierValue: Adult Classifier score. The score is in a range of [0-1.0] where 0 is least likely and 1.0 is most likely.
- TimeTakenMs: Time taken to execute the classification on the server.
- Resized: Flag indicating whether or not the resize operation was performed.

The XML looks like this:

	<ClassifierResult>
		<InputFileName>test.mp4</InputFileName>
      	<FileSize>6365770</FileSize>
      	<AdultClassifierValue>0.21175046251105303</AdultClassifierValue>
      	<TimeTakenMs>7642</TimeTakenMs>
      	<Resized>true</Resized
	</ClassifierResult>
	
