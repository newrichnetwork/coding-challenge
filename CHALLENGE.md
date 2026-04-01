# Coding Challenge

## Overview

You are given a PHP snippet that fetches data from an API and returns formatted results. Your task is to implement this functionality in a clean and well-structured way, and write tests for it.

## Environment

- You can use Composer to manage dependencies
- Tests should run with `composer test` (Pest PHP framework is recommended, but not required)
- An API server can be run locally if needed
- You may include any setup instructions in your README

## The Code

Here is the code snippet to implement:

```php
<?php

class ApiFetcher
{
    private $url = 'http://localhost:8000';
    private $logFile = '/tmp/api_log.txt';

    public function getData()
    {
        $ch = curl_init();
        curl_setopt($ch, CURLOPT_URL, $this->url);
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        $response = curl_exec($ch);

        if (!$response) {
            $this->log('Error fetching data: ' . curl_error($ch));
            return [];
        }

        $decoded = json_decode($response);
        curl_close($ch);

        if (!$decoded) {
            $this->log('Error decoding JSON');
            return [];
        }

        $results = [];
        foreach ($decoded as $item) {
            if ($item->active) {
                $results[] = strtoupper($item->name);
            }
        }

        return $results;
    }

    private function log($message)
    {
        file_put_contents($this->logFile, date('c') . ' ' . $message . PHP_EOL, FILE_APPEND);
    }
}

$fetcher = new ApiFetcher();
$data = $fetcher->getData();
print_r($data);
```

## Your Task

1. Implement this functionality in a structured way (e.g., using classes, services, etc.)
2. Organize your code as you see fit
3. Write tests to validate your implementation

## Constraints

- You may use any standard PHP 8.2+ features
- You are free to structure the project as you prefer
- You may add dependencies if needed (please justify them)
- Feel free to improve or extend the solution where appropriate
- As a guideline, try not to spend more than 60 minutes on this task

## Evaluation Criteria

Your solution will be evaluated based on:

- Correctness
- Code quality and structure
- Testing approach
- Clarity of your decisions

## Submission

1. Create a public GitHub repository with your solution
2. Include clear instructions on how to run your project
3. Add a short explanation in your README covering:
   - Assumptions you made
   - Design decisions
   - Trade-offs considered

4. Send us the link to your repository

Good luck!
